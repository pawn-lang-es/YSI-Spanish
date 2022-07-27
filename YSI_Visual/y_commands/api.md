#### _Command_IsEmptySlot
>* **Parámetros:**
> * `idx`: idx_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Prueba si la ranura dada está vacía.
 
***
#### _Comando_IsAlt
>* **Parámetros:**
> * `idx`: idx_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Prueba si la ranura dada es un comando alternativo.
 
***
#### _Comando_GetReal
>* **Parámetros:**
> * `ptr`: ptr_INFO
> * `idx`: idx_INFO
> * `name`: name_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Encuentra la versión original de un comando alt.  Actualizado para no contener largas
> cadenas largas (junto con "Command_AddAlt").
 
***
#### Command_OnReceived
>* **Parámetros:**
> * `error`: error_INFO
> * `playerid`: playerid_INFO
> * `cmdtext`: cmdtext_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Llama a OnPlayerCommandReceived una vez que el sistema sabe que el jugador puede usar
> este comando (si es que puede).  El orden de los parámetros es tal que el
> error es el primero.  Esto se debe a que se concatenan en tiempo de compilación para hacer
> error, y poner ese parámetro primero significa que no tenemos que omitir el espacio
> no necesitamos omitir el espacio después de cualquier coma.
 
***
#### _Comando_IsActive
>* **Parámetros:**
> * `comando`: comando_INFO
>* **Devuelve:**
> *¿Está activo el ID de este comando?
>* **Comentarios:**
> No hace ninguna comprobación de límites - use "_Command_IsValid" para eso.
 
***
#### _Command_IsValid
>* **Parámetros:**
> * `command`: command_INFO
>* **Devuelve:**
> * ¿Es válido el ID de este comando?
>* **Comentarios:**
> Comprobación interna de acceso directo.
 
***
#### _Comando_EsPrefijo
>* **Parámetros:**
> > `idx`: idx_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Comprueba si un carácter es un posible prefijo.  Puede utilizar una
> comparación sin signo.
 
***
#### _Comando_GetPrefix
>* **Parámetros:**
> * `c`: c_INFO
>* **Devuelve:**
> * El prefijo para este comando.
>* **Comentarios:**
> -
 
***
#### Nombre_del_comando
>* **Parámetros:**
> * `f`: f_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> -
 
***
#### Command_GetID
>* **Parámetros:**
> * `función[]`: función[]_INFO
>* **Devuelve:**
> * El ID de la función pasada.
>* **Comentarios:**
> -
> Command_GetID(function[]) nativo
 
***
#### Command_AddAlt
>* **Parámetros:**
> * `oidx`: oidx_INFO
> * `cmd[]`: cmd[]_INFO
>* **Devuelve:**
> * El ID del comando.
>* **Comentarios:**
> -
 
***
#### Command_ReProcess
>* **Parámetros:**
> * `playerid`: playerid_INFO
> * `cmdtext[]`: cmdtext[]_INFO
> * `help`: help_INFO
>* **Devuelve:**
> * true - éxito o fallo oculto.
> * false - fallo.
>* **Comentarios:**
> Hace todo el manejo de comandos y errores.
 
***
#### Command_GetPlayer
>* **Parámetros:**
> * `command`: command_INFO
> * `playerid`: playerid_INFO
>* **Devuelve:**
> * ¿Puede este jugador utilizar este comando?
>* **Comentarios:**
> bool nativo:Command_GetPlayer(command, playerid);
 
***
#### Command_GetPlayerNamed
>* **Parámetros:**
> * `funcname[]`: funcname[]_INFO
> * `playerid`: playerid_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Como Command_GetPlayer pero para un nombre de función.
> bool nativo:Command_GetPlayerNamed(funcname[], playerid);
 
***
#### Command_SetPlayer
>* **Parámetros:**
> * `command`: command_INFO
> * `playerid`: playerid_INFO
> * `bool:set`: bool:set_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> bool nativo:Command_SetPlayer(command, playerid, bool:set);
 
***
#### Command_SetPlayerNamed
>* **Parámetros:**
> * `funcname[]`: funcname[]_INFO
> * `playerid`: playerid_INFO
> * `set`: set_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Como Command_SetPlayer pero con un nombre de función.
> bool nativo:Command_SetPlayerNamed(funcname[], playerid, bool:set);
 
***
#### Command_Find
>* **Parámetros:**
>* `cmd[]`: cmd[]_INFO
>* **Devuelve:**
> * La ranura del array de este comando, o -1.
>* **Comentarios:**
> -
 
***
#### Command_AddAltNamed
>* **Parámetros:**
> * `function[]`: function[]_INFO
> * `altname[]`: altname[]_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Añadir un comando alternativo para un comando existente.
> Command_AddAltNamed(function[], altname[]) nativo;
 
***
#### Command_Remove
>* **Parámetros:**
> * `func`: func_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Command_Remove(func) nativo;
 
***
#### Command_RemoveNamed
>* **Parámetros:**
> * `func`: func_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Command_RemoveNamed(string:func[]) nativo;
 
***
#### Command_IsValid
>* **Parámetros:**
> * `command`: command_INFO
>* **Devuelve:**
> * ¿Es válido el ID de este comando?
>* **Comentarios:**
> -
 
***
#### Command_GetCurrent
>* **Parámetros:**
>* **Devuelve:**
> * El comando que se está procesando actualmente, o "COMMAND_NOT_FOUND".
>* **Comentarios:**
> -
 
***
#### Command_GetPlayerCommandCount
>* **Parámetros:**
> * `playerid`: playerid_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Obtiene el número de comamnds que este jugador puede utilizar.
> Command_GetPlayerCommandCount(playerid) nativo;
 
***
#### Command_GetName
>* **Parámetros:**
> * `f`: f_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Command_GetName(funcid) nativo;
 
***
#### Command_GetDisplay
>* **Parámetros:**
> * `f`: f_INFO
> * `p`: p_INFO
>* **Devuelve:**
> * El nombre de un comando para un solo jugador.
>* **Comentarios:**
> Abstracto porque hay un fallo cuando la cadena devuelve una cadena desde una
> función ajena (ver "Command_GetDisplayNamed").
> Command_GetDisplay(funcid, playerid) nativo;
 
***
#### Command_GetDisplayNamed
>* **Parámetros:**
> * `f[]`: f[]_INFO
> * `p`: p_INFO
>* **Devuelve:**
> * El nombre de una función con nombre para un jugador.
>* **Comentarios:**
> Llamada a la función remota para Command_GetDisplayNameNamed - evita tener que
> exponer a los usuarios a la extraña forma de devolver cadenas del sistema principal.  Esta es
> la única parte que aún no he arreglado para que sea bonita y oculta.
> cadena nativa:Command_GetDisplayNamed(cadena:funcid[], playerid);
 
***
#### Command_GetNext
>* **Parámetros:**
> * `index`: index_INFO
> * `playerid`: playerid_INFO
>* **Devuelve:**
> * El nombre de un comando para un solo jugador.
>* **Comentarios:**
> -
> Command_GetNext(index, playerid) nativo;
 
***
#### Comando
>* **Parámetros:**
> * `start`: start_INFO
>* **Devuelve:**
> * El siguiente comando.
>* **Comentarios:**
> Implementación interna del iterador "Command()" para "foreach".  Devuelve
> Todos los comandos que existen.  Normalmente las funciones de iterador toman dos
> parámetros, pero esta sólo necesita uno.  Realmente es muy simple, pero probablemente
> más rápido de esta manera ya que tiene acceso a la información interna.
 
***
#### PlayerCommand
>* **Parámetros:**
> * `pid`: pid_INFO
> > `start`: start_INFO
>* **Devuelve:**
> * El siguiente comando.
>* **Comentarios:**
> Implementación interna del iterador "PlayerCommand()" para "foreach".
> Devuelve todos los comandos que este jugador puede utilizar.
> Esto es similar a "Command_GetNext", pero devuelve un ID y no una cadena - Yo
> en realidad creo que esta forma es ligeramente mejor.
 
***
#### Command_GetPrefix
>* **Parámetros:**
> * `c`: c_INFO
>* **Devuelve:**
> * El prefijo para este comando ('/' por defecto).
>* **Comentarios:**
> -
 
***
#### Command_IsValidPrefix
>* **Parámetros:**
> * `prefix`: prefix_INFO
>* **Devuelve:**
> * ¿Es este un carácter válido para un prefijo?
>* **Comentarios:**
> ¡Este es el Único lugar donde se define la lista de prefijos válidos!  Son
> símbolos, no un alfanumérico, y bajo 128.
 
***
#### Command_IsPrefixUsed
>* **Parámetros:**
> * `prefijo`: prefix_INFO
>* **Devuelve:**
> * ¿Es un prefijo utilizado para algún comando?
>* **Comentarios:**
> -
 
***
#### Command_FlushPrefixes
>* **Parámetros:**
> * `prefix`: prefix_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Si un comando usa un prefijo y luego DEJA de usar dicho prefijo, la lista global
> de prefijos válidos tendrá que ser actualizada.
 
***
#### Command_SetPrefix
>* **Parámetros:**
> * `c`: c_INFO
> * `prefijo`: prefix_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Cambiar qué comando escribir "/x" vs "#x" por ejemplo.
 
***
#### Command_SetPrefixNamed
>* **Parámetros:**
> * `c`: c_INFO
> * `prefix`: prefix_INFO
>* **Devuelve:**
> * -
>* **Comentarios:**
> Cambiar qué comando escribir "/x" vs "#x" por ejemplo.
 
***
#### Command_OnPlayerText
>* **Parámetros:**
> * `playerid`: playerid_INFO
> * `text[]`: text[]_INFO
>* **Devuelve:**
> * 0 - No se ha podido procesar el comando.
> * 1 - Llamada al comando.
>* **Comentarios:**
> Se utiliza para implementar prefijos de comandos alternativos.
 
***
#### Command_OnPlayerCommandText
>* **Parámetros:**
> * `playerid`: playerid_INFO
> * `cmdtext[]`: cmdtext[]_INFO
>* **Devuelve:**
> * 0 - No se ha podido procesar el comando.
> * 1 - Llamada al comando.
>* **Comentarios:**
> El núcleo del procesador de comandos.  Ahora vsatly simplificado.
> Esta función primero encuentra el comando en nuestro mapa hash.  Si existe, comprueba
> comprueba si el jugador puede usarlo.  Si puede, comprueba si sólo está en el script actual.
> el script actual.  Si lo está, lo llama directamente, si no lo está, lo llama
> Si lo está, lo llama directamente, si no lo está, lo llama usando "CallRemoteFunction", que tiene en cuenta los estados maestros en
> múltiples scripts y el maestro especial 23, que lo llama sólo en un
> otro script.
 
***
#### HANDOFF
>* **Parámetros:**
>* **Devuelve:**
> * -
>* **Comentarios:**
> Pasa datos de comandos adicionales al nuevo maestro.
 
***
#### _Command_Rebuild
>* **Parámetros:**
>* **Devuelve:**
> * -
>* **Comentarios:**
> Reconstruye el hashmap de punteros de comandos después de la entrega de un script maestro.
 
***
#### Command_IncOPCR
>* **Parámetros:**
>* **Devuelve:**
> * -
>* **Comentarios:**
> Esta función, y las otras tres relacionadas, incrementan y disminuyen el
> número de devoluciones de llamada que se sabe que existen en el servidor.  Si son 0, no tiene sentido
> Si son 0, no tiene sentido intentar llamarlas en caso de error, etc.
 
***
#### Command_GetEmptySlot
>* **Parámetros:**
>* **Devuelve:**
> * La primera ranura disponible en "YSI_g_sCommands".
>* **Comentarios:**
> -
 
***
#### Command_Add
>* **Parámetros:**
> * `cmd[]`: cmd[]_INFO
> * `ptr`: ptr_INFO
> * `id`: id_INFO
>* **Devuelve:**
> * El ID del comando.
>* **Comentarios:**
> Esta era una función de la API externa, pero no hay razón para que lo sea ya que
> se llama para todos los comandos encontrados al inicio del modo.
 
***
#### _Command_GetDisplay
>* **Parámetros:**
> * `f`: f_INFO
> * `p`: p_INFO
>* **Devuelve:**
> * El nombre de un comando para un solo jugador.
>* **Comentarios:**
> -
 
***