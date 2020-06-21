La finalidad de este playbook es poder ansibilizar la instalación en diversos nodos simultáneamente de un script en lenguaje shell que permita la liberación de espacio ocupado de logs en FS, cuya instalación se adapte en función de los paths a truncar/comprimir que realmente existen en los nodos donde se instale.


* El funcionamiento del playbook es el siguiente:

Realiza checks de directorios, archivos y versión de OS previos a la instalación relativos al funcionamiento final del script.

* El funcionamiento del script instalado es el siguiente:

 -Truncado
  Únicamente se truncarán los logs objetivos del script si existe espacio disponible en el directorio auxiliar 'auxPath'. En concreto, se copia el log objetivo 'logs.path' al directorio auxiliar, se comprime, se concatena la fecha del dia actual al nombre del archivo, se vacía el log objetivo y se devuelve al directorio inicial. 
  
 -Compresión
  Mediante la variable 'logs.wildcard' se define el log o conjunto de logs mediante wildcard en el que se ejecutará la operación de comprimir sin rotar.
 
Los logs rotados pertenecerán a diversos tipos de aplicaciones:

Aplicaciones
 -LOGS: Opción de truncado y compresión customizable. El script en lenguaje shell realiza las operaciones definidas en los puntos Truncado y Compresión comentados anteriormente. Actualmente NO elimina archivos para liberar espacio, únicamente trunca y comprime, por lo que el problema de ocupación puede no solventarse por completo.
 
 -IHS: Realiza la misma operación de truncado que la definida en Truncado y Compresión para LOGS, pero es un proceso transparente para el usuario. Únicamente se necesita establecer su valor a 'true'.
 
 -WAS: Realiza la misma operación de truncado que la definida en Truncado y Compresión para LOGS, pero es un proceso transparente para el usuario. Únicamente se necesita establecer su valor a 'true'.

Uso de variables:

| Variable | Mandatory | Optional | Accepted values |
| ------ | ------ | ------ | ------ |
| installPath | x |  | '/ruta/a/script.sh' |
| auxPath | x |  |  /ruta_auxiliar| 
| minLogSize |x| | numeros naturales [0,1,...] en Bytes |
| IHS | |x| true/false |
| WAS | |x| true/false |
| logs.path | |x| '/ruta/a/log' |
| logs.wildcard| |x| '/ruta/a/????/log*' |

Nota: No está contemplado el uso de la variable 'logs.wildcard' sin el uso de 'logs.path'.
Por defecto, los permisos del script es:
 
 rw-r-xr-x root:sys 

