# YSI

## Información general

* [Instalación](instalacion.md)
* [Solución de problemas](solucion-problemas.md)
* [Compatibilidad (YSI_COMPATIBILITY_MODE)](YSI_COMPATIBILITY_MODE.md)

## Librerías

Las librerías están divididas aproximadamente por uso.  Cada una está incluída por grupo y nombre, por lo que para incluir *y_va*, la cuál está en *Coding* usa:

```pawn
#include <YSI_Coding\y_va>
```

Aunque YSI provee un montón de librerías, no estarán incluidas a menos de que las incluyas. Por lo que si no necesitas *y_zonepulse* solo no la incluyas y no aparecerá en tu proyecto por completo. Esto significa que YSI puede contener un montón de funciones, pero son todas opcionales.

### Coding

Mejoras a la escritura de scripts en PAWN (por ejemplo, nuevas características del lenguaje).

* [y_ctrl](YSI_Coding/y_ctrl.md)
* [y_cgen](YSI_Coding/y_cgen.md)
* [y_functional](YSI_Coding/y_functional.md)
* [y_hooks](YSI_Coding/y_hooks.md)
* [y_inline](YSI_Coding/y_inline.md)
* [y_malloc](YSI_Coding/y_malloc.md)
* [y_remote](YSI_Coding/y_remote.md)
* [y_stringhash](YSI_Coding/y_stringhash.md)
* [y_timers](YSI_Coding/y_timers.md)
* [y_unique](YSI_Coding/y_unique.md)
* [y_va](YSI_Coding/y_va.md)

### Core

Librerías principales, usadas en casi todos lados.

* [y_als](YSI_Core/y_als.md)
* [y_cell](YSI_Core/y_cell.md)
* [y_compilerdata](YSI_Core/y_compilerdata.md)
* [y_debug](YSI_Core/y_debug.md)
* [y_master](YSI_Core/y_master.md)
* [y_profiling](YSI_Core/y_profiling.md)
* [y_testing](YSI_Core/y_testing.md)
* [y_utils](YSI_Core/y_utils.md)

### Data

Manipulación de datos, estructura de datos y algoritmos.

* [y_bintree](YSI_Data/y_bintree.md)
* [y_bit](YSI_Data/y_bit.md)
* [y_circular](YSI_Data/y_circular.md)
* [y_iterate](YSI_Data/y_iterate.md) (AKA y_foreach)
* [y_hashmap](YSI_Data/y_hashmap.md)
* [y_jaggedarray](YSI_Data/y_jaggedarray.md)
* [y_percent](YSI_Data/y_percent.md)
* [y_playerarray](YSI_Data/y_playerarray.md)
* [y_playerset](YSI_Data/y_playerset.md)
* [y_sortedarray](YSI_Data/y_sortedarray.md)
* [y_sparsearray](YSI_Data/y_sparsearray.md)

### Extra

Características opcionales.

* [y_extra](YSI_Extra/y_extra.md)
* [y_files](YSI_Extra/y_files.md)
* [y_streamer_plugin](YSI_Extra/y_streamer_plugin.md)

### Game

Librerías que proveen información sobre el juego.

* [y_vehicledata](YSI_Game/y_vehicledata.md)

### Players

Librerías para la gestión de jugadores.

* [y_android](YSI_Players/y_android.md)
* [y_groups](YSI_Players/y_groups.md)
* [y_languages](YSI_Players/y_languages.md)
* [y_text](YSI_Players/y_text.md)
* [y_users](YSI_Players/y_users.md)

### Server

Librerías para controlar el servidor.

* [y_colours](YSI_Server/y_colours.md) (AKA y_colors)
* [y_files](YSI_Server/y_files.md)
* [y_flooding](YSI_Server/y_flooding.md)
* [y_lock](YSI_Server/y_lock.md)
* [y_punycode](YSI_Server/y_punycode.md)
* [y_scriptinit](YSI_Server/y_scriptinit.md)
* [y_stringise](YSI_Server/y_stringise.md) (AKA y_stringize)
* [y_td](YSI_Server/y_td.md)

### Storage

Librerías para interactuar con datos persistentes.

* [y_amx](YSI_Storage/y_amx.md)
* [y_bitmap](YSI_Storage/y_bitmap.md)
* [y_ini](YSI_Storage/y_ini.md)
* [y_php](YSI_Storage/y_php.md)
* [y_svar](YSI_Storage/y_svar.md)
* [y_uvar](YSI_Storage/y_uvar.md)
* [y_xml](YSI_Storage/y_xml.md)

### Visual

Librerías que tienen efectos visibles dentro del juego.

* [y_areas](YSI_Visual/y_areas.md)
* [y_classes](YSI_Visual/y_classes.md)
* [y_commands](YSI_Visual/y_commands.md)
* [y_dialog](YSI_Visual/y_dialog.md)
* [y_loader](YSI_Visual/y_loader.md)
* [y_properties](YSI_Visual/y_properties.md)
* [y_races](YSI_Visual/y_races.md)
* [y_zonenames](YSI_Visual/y_zonenames.md)
* [y_zonepulse](YSI_Visual/y_zonepulse.md)

## ¿Qué significan las siglas YSI?

¡Nadie lo sabe! La idea original era *Inclusiones al servidor de Y_Less* ("Y_Less' Server Includes"), pero había confusión con la letra 'S', y hay más desarrolladores que solo Y_Less ahora mismo, entonces la "Y" solo se convierte en un acrónimo recursivo para "YSI".  Ahora hay diferentes significados oficiales, cada uno incorporando diferentes aspectos de YSI:

### YSI Script Includes

Librerías principales.

### YSI Scripting Improvements

Librerías de codificación (extensiones al lenguaje Pawn).

### YSI Server Includes

Aspectos relacionados al modo de juego (comandos, propiedades, texto, etc).

### YSI Script Incidentals

Extras, como las librerías para iniciar sesión y los comandos.

### YSI Seriously Incomprehensible

Los macros (aunque en su defensa, escribir macros para hacer el parsing dentro de los límites del compilador es MUY difícil).