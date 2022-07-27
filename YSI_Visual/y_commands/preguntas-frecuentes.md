# Preguntas

## ¿Por qué no puedo llamar a los comandos directamente?

Con ZCMD puedes hacer:

``pawn
CMD:MiComando(playerid, params[])
{
	return cmd_MiOtroComando(playerid, params);
}
CMD:MiOtroComando(playerid, params[])
{
	SendClientMessage(playerid, COLOUR_GREETING, "Hi");
	return 1;
}
```

Esto es un error en y_commands. y_commands tiene soporte nativo para nombres de comandos alternativos, por lo que la forma correcta de hacer esto es:

```pawn
hook OnScriptInit()
{
	Command_AddAlt(YCMD:MyOtherCommand, "MyCommand");
}
YCMD:MiOtroComando(playerid, params[])
{
SendClientMessage(playerid, COLOUR_GREETING, " Hola");
	return 1;
}
```

O (en YSI 5.x):

```pawn
YCMD: MiComando(playerid, params[], help) = MiOtroComando;
YCMD: MiOtroComando(playerid, params[], help)
{
    SendClientMessage(playerid, COLOUR_GREETING, " Hola");
	return 1;
}
```

## ¿Pero cómo los llamo desde algo que no sea otro comando?

No se puede.

## ¿Por qué?

Esto es objetivamente una mala práctica de codificación.  Ya hay formas bien definidas de llamar al código desde otro código - ¡se llaman funciones!  Los comandos son una interfaz para el mundo exterior (es decir, los jugadores), una vez que estás en el código no los necesitas.  Los parámetros se pasan a los comandos a través de cadenas de caracteres, que son difíciles de tratar (de ahí `sscanf` y otras herramientas), pero los parámetros en el código real son fáciles de tratar.

El código para hacer la misma cosa tanto en un comando con ZCMD como haciendo clic en un jugador podría tener el siguiente aspecto

``pawn
CMD:arrest(playerid, params[])
{
	if (!IsPlayerCop(playerid))
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No eres un policía!");
	new targetid;
	if (sscanf(params, "u", targetid) | targetid == INVALID_PLAYER_ID)
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No se pudo encontrar el objetivo!");
	// Ponerlos en la cárcel.
	SetPlayerPos(targetid, 1084.3, 2250.6, 503.4);
	SendClientMessage(playerid, COLOUR_GREETING, "¡Jugador detenido!");
	SendClientMessage(targetid, COLOUR_GREETING, "¡Has sido arrestado!");
	return 1;
}
public OnPlayerClickPlayer(playerid, clickedplayerid, source)
{
	new params[16];
	format(params, sizeof (params), "%d", clickedplayerid);
	return cmd_arrest(playerid, params);
}
```

Hay varios problemas con este código:

1. Conviertes un número en una cadena, para pasarlo al comando, para convertirlo de nuevo en un número.  Esto es sólo un desperdicio de esfuerzo, también se salta la comprobación de tipos del compilador.
2. Asume que los permisos para ambos son los mismos.  Si sólo los detectives pueden hacer clic en los nombres para arrestar, esto se convierte en:

``pawn
static bool:gCalledFromClick = false;
CMD:arrest(playerid, params[])
{
	if (!gCalledFromClick && !IsPlayerCop(playerid))
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No eres un policía!");
	new targetid;
	if (sscanf(params, "u", targetid) | targetid == INVALID_PLAYER_ID)
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No se pudo encontrar el objetivo!");
	// Ponerlos en la cárcel.
	SetPlayerPos(targetid, 1084.3, 2250.6, 503.4);
	SendClientMessage(playerid, COLOUR_GREETING, "¡Jugador detenido!");
	SendClientMessage(targetid, COLOUR_GREETING, "¡Has sido arrestado!");
	devolver 1;
}
public OnPlayerClickPlayer(playerid, clickedplayerid, source)
{
	if (!IsPlayerDetective(playerid))
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No eres un detective!)
	new params[16];
	format(params, sizeof (params), "%d", clickedplayerid);
	gCalledFromClick = true;
	new ret = cmd_arrest(playerid, params);
	gCalledFromClick = false;
	return ret;
}
```

Necesitas añadir un montón de código extra para hacer los permisos, y el comando se infla porque necesita saber que puede ser llamado desde un clic, y que si es llamado desde un clic, para no hacer las comprobaciones de permisos.

El código se vuelve aún más complejo con y_commands y y_groups, porque las comprobaciones de permisos no se hacen en el propio comando:

```pawn
static Group:gGroupBypass;
static Group:gGroupCop;
static Group:gGroupDetective;
YCMD:arrest(playerid, params[], help)
{
	new targettid;
	if (sscanf(params, "u", targetid) || targetid == INVALID_PLAYER_ID)
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No se pudo encontrar el objetivo!");
	// Ponerlos en la cárcel.
	SetPlayerPos(targetid, 1084.3, 2250.6, 503.4);
	SendClientMessage(playerid, COLOUR_GREETING, "¡Jugador detenido!");
	SendClientMessage(targetid, COLOUR_GREETING, "¡Has sido arrestado!");
	return 1;
}
public OnPlayerClickPlayer(playerid, clickedplayerid, source)
{
	if (gGroupDetective < playerid)
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No eres un detective!");
	new cmdtext[16];
	format(cmdtext, sizeof (cmdtext), "/arrest %d", clickedplayerid);
	gGroupBypass += playerid;
	new ret = Command_ReProcess(playerid, cmdtext);
	gGroupBypass -= playerid;
	return ret;
}
public OnScriptInit()
{
	// Crea los grupos.
	gGroupBypass = Group_Create();
	gGroupCop = Group_Create("Policías");
	gGroupDetective = Group_Create("Detectives");
	
	// Desactivar el comando para los jugadores normales.
	Group_SetCommandDefault(YCMD:arrest, false);
	
	// Habilitar el comando para los policías, y la gente que utiliza el bypass de clic.
    Group_SetCommand(gGroupCop, YCMD:arrest, true);
	Group_SetCommand(gGroupBypass, YCMD:arrest, true);
}
```

## ¿Cuál es la solución?

La forma correcta de manejar esto, con y_commands, ZCMD, o cualquier otro código, es utilizar una tercera función.  Esta función hará la lógica de detención real, y las retrollamadas y comandos sólo proporcionarán una interfaz externa a esta función:

```pawn
DoArrest(playerid, targetid)
{
	// Ponerlos en la cárcel.
	SetPlayerPos(targetid, 1084.3, 2250.6, 503.4);
	SendClientMessage(playerid, COLOUR_GREETING, "¡Jugador detenido!");
	SendClientMessage(targetid, COLOUR_GREETING, "¡Has sido arrestado!");
}
YCMD:arrest(playerid, params[], help)
{
new targetid;
	if (sscanf(params, "u", targetid) || targetid == INVALID_PLAYER_ID)
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No se pudo encontrar el objetivo!");
	DoArrest(playerid, targetid);
	return 1;
}
public OnPlayerClickPlayer(playerid, clickedplayerid, source)
{
	if (gGroupDetective < playerid)
		return SendClientMessage(playerid, COLOUR_FAILURE, "¡No eres un detective!");
	DoArrest(playerid, clickedplayerid);
	return true;
}
```

Ahora estás aprovechando al máximo la potencia del compilador - esto es más rápido porque utiliza parámetros reales en lugar de cadenas, y puede comprobar que todos los parámetros son correctos.

## ¿Por qué `Command_ReProcess` no es `const`-correcto?

Hay dos razones:

1. La gente no hace sus comandos `const`-correctos:

```pawn
YCMD: micomando(playerid, params[], help)
{
}
```

Aquí, `params` no es `const`, y muy frecuentemente no lo es.  Hacer que `Command_ReProcess`, que llama a los comandos, sea `const`-correcto significaría ralentizar la función ligeramente para copiar los datos, o hacer que cada comando en todas partes sea `const`-correcto.  Otros procesadores de comandos pueden salirse con la suya porque utilizan un método de llamada más lento, que ya copia cosas.

2. Fomenta las malas prácticas:

Como se ha explicado anteriormente, no puedes llamar a los comandos directamente en y_commands, y no deberías poder hacerlo.  Hacer que `Command_ReProcess` sea `const`-correcto haría posible este código:

```pawn
Command_ReProcess("/micomando");
```

Esto es hacer lo incorrecto, y queremos que hacer lo incorrecto sea lo más difícil posible.  Ver [*Así que cuál es la solución*](#cual-es-la-solución) para saber qué hacer en su lugar.

## ¿No es `otro procesador de comandos` más rápido que esto?

Tal vez.  ¿Y? y_commands es tan rápido, o ligeramente más rápido, que la mayoría de los otros procesadores de comandos (si crees en sus gráficos, pero todos tienen una agenda), pero con muchas más características.

### Cómo hacer un procesador de comandos ligeramente más rápido:

1. Eliminar las comprobaciones:

> ZCMD tiene un montón de comprobaciones que no entiendo, deben ser inútiles.
2. Quitar características:

> Nadie quiere comprobar si un jugador puede usar este comando, lo eliminaré.
3. Trabajar realmente en los algoritmos involucrados.

Sólo y_commands se molesta con este.

### ¿Qué es lo que se está cronometrando?

La mayoría de los procesadores de comandos, cuando afirman que son más rápidos, sólo cronometran el tiempo que se tarda en LLAMAR al comando.  Una vez que la ejecución del código llega al comando, eso es todo.  ¿Pero qué ocurre dentro del comando?  Para la mayoría, lo primero que hacen es comprobar si un jugador puede utilizar el comando.  Esta comprobación de permisos no se incluye en el tiempo del procesador de comandos porque se considera parte del propio comando. y_commands, sin embargo, hace estas comprobaciones por ti, e incluye el tiempo que se tarda en hacer estas comprobaciones en sus informes.  A pesar de esta sobrecarga, sigue siendo más rápido que muchos procesadores de comandos.  Así que puede tener un procesador ligeramente más rápido y comandos mucho más lentos, o un procesador de comandos ligeramente más lento y comandos mucho más rápidos (porque el procesador hace el trabajo duro por usted).

Pero, de nuevo, no te dirán esto.