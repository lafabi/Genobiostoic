# Elaboración de Scripts en FRONTEND

Existen varias formas de ejecutar una tarea o correr un programa en la terminal de bash:

 1) A través de la introducción de una linea de comando directa luego del prompt, con el código del programa que se pretende correr. Esta acción inutiliza la ventana de la terminal donde se introdujo el código hasta que se termine de ejecutar la tarea que se solicitó. Una solución a esto, sería ocupar el ampersand "&" al final del código, lo que enviará el proceso a un segundo plano, activando la posibilidad de continuar trabajando en la terminal. Al enviar el trabajo en segundo plano con el "&", el sistema imprimirá un código numérico en pantalla que indica el ID de la tarea que se envió al sistema, y se podrá monitorizar a través su progreso con el comando ```htop```.

```
 htop
```

# Scripts en la maquina local

2) Por medio de un código escrito y almacenado en un archivo de texto plano *script*. Éste se define como un programa o código de programación escrito en un lenguaje específico (como R, Bash o Python), que se utiliza para realizar cálculos, análisis o procesamiento, en este caso particular, de datos biológicos. Los scripts son herramientas fundamentales en bioinformática, pues permiten, por ejemplo, automatizar tareas repetitivas a través de la aplicación de algoritmos. Dado que en el tutorial anterior aprendimos líneas de comando básicas en la terminal de Linux, haremos un script sencillo utilizando comandos ya conocidos. Para ello abriremos el editor de texto nano y, una vez abierto, tipearemos la orden de crear un directorio llamado Genobiostoic de la siguiente forma:
    
```
nano
mkdir Genobiostoic
```


Seguidamente guardaremos el documento de texto plano con el nombre de "script1.sh" y haremos el script ejecutable, es decir, que el sistema lo reconozca como un programa, a través del siguiente comando:
```
$chmod +x script1.sh
```
Observaremos, al listar de nuevo el contenido del directorio, que el nombre "script1.sh" ha cambiado de color, indicativo de que el documento que acabamos de crear ahora puede ser ejecutado como un programa con una instrucción específica de realizar una tarea.

Una vez realizado esto, podremos correr este script1 de varias formas:

2.1) Directo en la terminal; al igual que el apartado anterior, esta forma inutilizará la ventana hasta que se complete el proceso. Si se considera que se ejecutarán programas complejos se tardará aun más la operatividad de la ventana. De igual forma que el apartado anterior, se puede ocupar el ampersand "&" para correrlo en segundo plano. Para correr este script1.sh tipeamos en la terminal:
```
bash script1.sh
```
o
```
bash script1.sh&
```

2.2) Enviarlo al frontend (que es la interfaz con la que interactuamos en el sistema operativo) a través de un comando "nohup" y redireccionar los archivos de reporte de salida de la siguiente forma:
```
nohup ./script1.sh > script.out
```

Es muy conveniente correr los scripts con tareas complejas a través de esta forma, dado que si se produjera un error en el procesamiento del análisis saldría reportado en el archivo script.out, que crea automáticamente esta alternativa. De hecho, durante el tiempo de la corrida se puede verificar el progreso en tiempo real del avance del programa. Para esto sólo debemos correr el siguiente comando para imprimir el contenido del archivo:
```
cat script.out
```
En ambos casos, al listar de nuevo el contenido del directorio donde estamos ubicados, aparecerá ya creado un directorio con el nombre "Genobiostoic".



