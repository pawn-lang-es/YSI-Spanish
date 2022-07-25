# YSI_COMPATIBILITY_MODE

Este es un modo de compilación especial, activado con la bandera `YSI_COMPATIBILITY_MODE`:

```pawn
// Al comienza de tu script.
#define YSI_COMPATIBILITY_MODE

// Todos los demás includes y deficiones siguen acá.
```

O `YSI_COMPATIBILITY_MODE=1` en la línea de comandos.

Desactiva toda la sintaxis personalizada y palabras reservadas de YSI, reemplazándolas
con sus versiones *todo-en-mayúscula* y *sufijo-doble-guión-bajo*:

```pawn
TIMER__ SayHi[1000](playerid)
{
	SendClientMessage(playerid, COLOUR_GREETING, "Hola!");
}

HOOK__ OnPlayerConnect(playerid)
{
	DEFER__ SayHi(playerid);
}
```

Esto reduce el chance de cualquier colisión de símbolos con otra librería o include. Por
ejemplo, YSI y pawn-plus, ambas incluyen un palabra reservada `yield`, y hay diferentes 
versiones de `foreach`.

En este modo, aún puedes usar las palabras reservadas normales activándolas explicitamente:

```pawn
#define YSI_COMPATIBILITY_MODE
#define YSI_KEYWORD_hook

#include <a_samp>
#include <YSI_Coding\y_hooks>
#include <YSI_Coding\y_timers>

TIMER__ SayHi[1000](playerid)
{
	SendClientMessage(playerid, COLOUR_GREETING, "Hola!");
}

hook OnPlayerConnect(playerid)
{
	DEFER__ SayHi(playerid);
}
```

De forma alternativa, si quieres todas, pero menos una de ellas, puedes dejar el modo de
compatibilidad desactivado y solo inhabilitar una palabra reservada:

```pawn
#define YSI_NO_KEYWORD_hook

#include <a_samp>
#include <YSI_Coding\y_hooks>
#include <YSI_Coding\y_timers>

timer SayHi[1000](playerid)
{
	SendClientMessage(playerid, COLOUR_GREETING, "Hola!");
}

HOOK__ OnPlayerConnect(playerid)
{
	defer SayHi(playerid);
}
```

