# Características

## Declarando comandos

```pawn
YCMD:me(playerid, params[], help)
{
	if (isnull(params))
		return SendClientMessage(playerid, COLOUR_FAILURE, "Debes introducir una acción");
    new str[144];
	format(str, sizeof (str), "** %s %s **", ReturnPlayerName(playerid), params);
	return SendClientMessageToAll(COLOUR_GREETING, str);
}
```

## Declarar nombres de comandos alternativos

```pawn
YCMD:i(playerid, params[], help) = me;
```

## Información de ayuda

```pawn
YCMD:me(playerid, params[], help)
{
	if (help)
		return SendClientMessage(playerid, COLOUR_GREETING, "Role-play una acción. Ejemplo: '/me salta'");
	if (isnull(params))
		return SendClientMessage(playerid, COLOUR_FAILURE, "Debes introducir una acción");
	new str[144];
	format(str, sizeof (str), "** %s %s **", ReturnPlayerName(playerid), params);
	return SendClientMessageToAll(COLOUR_GREETING, str);
}
```

## Permisos

```pawn
nuevo Grupo:gGroupLoggedIn;
public OnScriptInit()
{
	// Crea un grupo para las personas que han iniciado sesión.
	gGroupLoggedIn = Group_Create();
	// Desactivar todos los comandos por defecto.
	Group_SetGlobalCommandDefault(false);
	// Habilitar el comando sólo para las personas de este grupo.
	Group_SetCommand(gGroupLoggedIn, YCMD:me, false);
}
public OnPlayerLogIn(playerid)
{
	// Añade el jugador al grupo - ahora pueden usar `/me`.
	gGroupLoggedIn += playerid;
}
```