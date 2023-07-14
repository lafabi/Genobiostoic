# Elaboración de Scripts

Existen varias formas de ejecutar una tarea o correr un programa en la terminal de  bash:

 1) A través de la introducción de una linea de comando directa luego del prompt,con el código del programa que se pretende correr. Esta acción inutiliza la ventana de la terminal donde se introdujo el código hasta que se termine de ejecutar la tarea que se solicitó. Una solución a esto, sería ocupar el and person "&" al final del código, esto enviará el proceso en segundo plano y se activa el la posibilidad de continuar trabajando en la terminal. Al enviar el trabajo en segundo plano con el "&" el sistema imprimirá un código numérico en pantalla que indica el ID de la tarea que se envió al sistema y se podrá monitorizar a través su progreso con el comando ```htop```.

```
 htop
```

#Scripts en la maquina local

 2) Por medio de un código escrito y almacenado en "script". Éste se define como un programa o código de programación escrito en un lenguaje específico (como R, Bash o Python),que se utiliza para realizar cálculos, análisis o procesamiento, en este caso paricular,de datos biológicos. Los scripts son herramientas fundamentales en en bioinformática, pues permiten, por ejemplo, automatizar tareas repetitivas a través de la aplicación de algoritmos.Dado que en el tutorial anterior aprendimos lineas de comando básicas en la terminal de Linux, haremos un script sencillo utilizando comandos ya conocidos. Para ello abriremos el editor de texto nano y tipearemos la orden de crear un directorio llamado sochigen de esta forma:
    
```
nano
```
mkdir sochigen

Seguidamente guardaremos el documento de texto plano con el nombre de "script1.sh" y haremos el script ejecutable, es decir el sistema lo reconocerá como un programa, a través del siguiente comando:
```
$chmod +x script1.sh
```
Observaremos al listar de nuevo el contenido del directorio, que el nombre "script1.sh" ha cambiado de color, indicativo que el documento que acabamos de crear ahora puede ser ejecutado como un programa con una instrucción específica de realizar una tarea.

Una vez realizado esto, podremos correr este script1 de varias formas:

2.1) Directo en la terminal, al igual que el apartado anterior, esta forma inutilizará la ventana hasta que se complete el proceso, si se considera que se ejutará programas complejos se tardará aun más la operatividad de la ventana.De igual forma que el apartado anterior, se puede ocupar el and person "&" para correrlo en segundo plano.Para correr este script1.sh tipeamos en la terminal
```
bash script1.sh
```
o
```
bash script1.sh&
```

2.2) Enviarlo al frontend (que es la interfaz con la que interactuamos en sistema operativo) a través de un comando "nohup" y redireccionar los archivos de reporte de salida de la siguiente forma:
```
nohup ./script1.sh > script.out
```

Es muy conveniente correr los scripts con tareas complejos a través de esta forma, dado que si se produjera un error en el procesamiento del análisis, saldría reportado en el archivo script.out que crea automáticamente esta alternativa, de hecho durante el tiempo de la corrida, se puede verificar el progreso en tiempo real del avance del programa.Para esto sólo debemos correr el siguiente comando para imprimir el contenido del archivo:
```
cat script.out
```
En ambos casos, al listar de nuevo el contenido del directorio donde estamos ubicados, aparecerá ya creado un directorio con el nombre "sochigen"

# Scripts en Servidores Remotos

3)El uso de servidores remotos, es cada vez más común y posibilita la oportunidad de ocupar, eficientemente, múltiples procesadores de alto rendimiento. Al igual que nuestra máquina local, éstos servidores ofrecen la alternativa de correr scripts en el frontend, pero no es la mejor alternativa, dado que se ocupan los recursos informaticos de forma poco eficiente. En este caso, los servidores de alta capacidad tales como el NLHPC de la Universidad de Chile [https://www.nlhpc.cl/](https://www.nlhpc.cl/) o [Geryon https://www3.astro.puc.cl/geryon/](https://www3.astro.puc.cl/geryon) de la Universidad Católica funcionan con un sistema de planificador de tareas. Este sistema opera asignando filas y prioridades a las tareas según la capacidad de los recursos, administrando de mejor forma los recursos tales como memoria, núcleos, tiempo de ejecución de trabajos, etc. Estos scripts se corren en el backend, que es un espacio donde se llevan a cabo tareas en el sistema operativo oculto de fondo. En el próximo apartado hablaremos con más detalle de este sistema de administrador de trabajos. Por ahora veremos la arquitectura en la construcción de estos scripts: 

Al igual que una carta, los scripts que se envían al backend tienen un "membrete" con una serie de intrucciones para el asistente "virtual", en ésta indicarán ciertas características de la tarea. Un detalle importante para tener en cuenta a la hora de construir un script es que deben ser construidos en editores de texto plano,tales como nano,vim, gedit,notepad, entre otros. No se deben realizar scripts en programas de editor de texto con formato tipo word, pues los diferentes tipos de formatos (margen,sangría,tipo de letras, etc) serán reconocidos erróneamente por los programas. 

El script que se envía al NLHPC de la Universidad de Chile tiene la siguente estructura y puedes generarlo de forma online a través de esta página [https://wiki.nlhpc.cl/Generador_Scripts](https://wiki.nlhpc.cl/Generador_Scripts): 

```
#!/bin/bash
#---------------Script SBATCH - NLHPC ----------------
#SBATCH -J Fabiola
#SBATCH -p general
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem-per-cpu=4250
#SBATCH --mail-user=lafabileon@gmail.com
#SBATCH --mail-type=ALL
#SBATCH -t 2-2:2:5
#SBATCH -o Fabiola_%j.out
#SBATCH -e Fabiola_%j.err

#-----------------Toolchain---------------------------
# ----------------Modulos----------------------------
# ----------------Comando--------------------------
```

###Pensar en colocar la tabla, como imagen, de Leftrarú en este apartado.

Dependendiendo de los recursos que requiera el trabajo (nodos, hilos, memoria, tiempo), se escoje la partición en el servidor y se agrega la información necesaria para construir el "membrete" del script de forma muy sencilla y amigable.Una vez realizado se copia y se pega en un editor de texto plano, se adiciona el código comando que se quiere ejecutar y se asigna un nombre (e este caso script2.sh) junto con la extensión del lenguaje en que se ha escrito el script (en este caso bash, .sh). 

Una vez generado el script se lanza al backend, o  gestor de trabajos SLURM,  de la siguiente forma
```
$sbatch script2.sh
```

Y automáticamente se genera un ID JOB

$Submitted batch job 25489521
