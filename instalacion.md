# Instalación
Se recomienda usar **sampctl**

## Con *sampctl*
```pawn
sampctl package install pawn-lang/YSI-Includes@5.x
```

## Sin *sampctl*
Descarga la versión más reciente de la librería y sus dependencias de los siguientes enlaces:

Extrae el archivo comprimido *zip* YSI a la carpeta `includes/` (o donde guardes tus includes),
el *zip* amx_assembly a `includes/amx/`, el *zip* md-sort a `includes/md-sort/`, el *zip*
indirection a `includes/indirection/`, y el *zip* code-parse `includes/code-parse`.

## Opciones en momento de compilación
YSI muestra un montón de información cuando se carga. Puedes desactivar algunos con las siguientes
directivas:

```pawn
// No imprime el mensaje acerca del caché del código (con `YSI_YES_MODE_CACHE`).
#define YSI_NO_CACHE_MESSAGE

// No muestra el mensaje sobre la optimización al arrancar (todavía sucede, solo que no se te muestra).
#define YSI_NO_OPTIMISATION_MESSAGE

// No comprueba si esta es la última versión de YSI.
#define YSI_NO_VERSION_CHECK


#include <YSI_Grupo\y_libreria>
```

## Caché
Si tu proyecto se demora demasiado al arrancar, puedes puedes guardarlo en la memoria caché.
Esto pre-optimiza un montón del proyecto, y guarda el resultado en `scripfiles/YSI_CACHE.amx`.
Con esta función solo harías el arranque lento una vez y luego desplegar la versión rápida
a tu servidor.