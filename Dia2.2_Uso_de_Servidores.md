# Uso de Servidores de alta Capacidad


El uso de servidores remotos, es cada vez más común y posibilita la oportunidad de ocupar, eficientemente, múltiples procesadores de alto rendimiento. Cada servidor tiene su propio tipo de configuración, arquitectura, capacidades, particiones y pueden tener o no agendadores de tareas o Schedulers. Les sugerimos que a la hora de ocupar un servidor de alta capacidad, aprendan sobre su estructuración y funcionamiento a través de las instrucciones de sus administradores.
Una de las primeras tareas que debemos aprender para trabajar con servidores remotos es cómo conectarnos, para ello usamos el comando ```ssh``` (security shell), este comando nos permite hacer una conexión segura desde la máquina local a la remota, una vez abierta la cuenta en el servidor remoto, el administrador del servidor nos otorgará un usuario y un password, en muchas ocasiones necesitaremos una dirección IP para poder establecer la conexión:

Para usuarios de servidores de alta capacidad tal como el caso del NLHPC de la Universidad De Chile, nuestro usuario lucirá así: 

```fleon@leftraru.nlhpc.cl```
``` passw: XXXX```

Para el caso particular de servidores de remotos que no son de alta capacidad debemos contar con la dirección IP, en este caso el usuario lucirá de esta forma:
```usuario@146.155.227.140```
```passw: XXXX```

Para conectarnos basta colocar el comando ```ssh``` antes del usuario:

```
ssh usuario@leftraru.nlhpc.cl

```
Inmediatamente el servidor nos solicitará el password.

```usuario@146.155.227.140's password:```


En ocasiones, la primera vez que nos conectamos a un servidor remoto, éste nos solicita compartir una llave de seguridad para establecer una conexión segura de intercambio de archivos y transferencia de información, de esta forma puede aparecer un diálogo en pantalla y aceptaremos tipeando un *s*

Una vez conectado en el servidor, entraremos al *home* del usuario hospedero, que en este caso es ```fleon```. Al ingresar listaremos el contenido del directorio con ```ls``` y veremos el siguiente contenido: 

![Z.png](https://github.com/lafabi/Genobiostoic/blob/main/Z.png)


Nos cambiaremos al directorio *usuarios* y para cada participante crearemos un directorio con su nombre usando ```mkdir```. Verificamos que cada nombre del ususrio escogido por participante se haya creado dentro de /home/fleon/usuario a través del comando ```ls```


Al igual que nuestra máquina local, éstos servidores ofrecen la alternativa de correr scripts en el **frontend**, pero no es la mejor opción , dado que se ocupan los recursos informaticos de forma poco eficiente. En este caso, los servidores de alta capacidad tales como el NLHPC de la Universidad de Chile [https://www.nlhpc.cl/](https://www.nlhpc.cl/) o [Geryon https://www3.astro.puc.cl/geryon/](https://www3.astro.puc.cl/geryon) de la Universidad Católica funcionan con un sistema de planificador de tareas o Schedulers. Este sistema opera asignando filas y prioridades a las tareas según la capacidad de los recursos, administrando de mejor forma los recursos tales como memoria, núcleos, tiempo de ejecución de trabajos, etc. Estos scripts se corren en el **backend**, que es un espacio donde se llevan a cabo tareas en el sistema operativo oculto de fondo. En el próximo apartado hablaremos con más detalle de este sistema de administrador de trabajos. Por ahora veremos la arquitectura en la construcción de estos scripts: 

Al igual que una carta, los scripts que se envían al backend tienen un "membrete" con una serie de intrucciones para el asistente "virtual", en ésta indicarán ciertas características de la tarea. 

Un detalle importante para tener en cuenta a la hora de construir un script es que deben ser construidos en editores de texto plano, tales como nano, vim, gedit, notepad, entre otros. No se deben realizar scripts en programas de editor de texto con formato tipo word, pues los diferentes tipos de formatos (margen, sangría, tipo de letras, etc) serán reconocidos erróneamente por los programas. 

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

El *Toolchain* se refiere a las variables del entorno que se quieran definir para definir las rutas de archivos de entrada y rutas de archivos de salida y cómo pueden estar enlazados unos con otros.

Los *Módulos* se refieren a unidades funcionales y estructurales que forman parte de programas o software diseñados para analizar datos.
Los *Comandos* son las instrucciones que le otorgamos al sistema ejecutar bajo ciertos parámetros que el usuario diseña. Veremos más adelante con un ejemplo cómo contruir un script para la verificación de calidad de los genomas.

Dependendiendo de los recursos que requiera el trabajo (nodos, hilos, memoria, tiempo), se escoje la partición en el servidor y se agrega la información necesaria para construir el "membrete" del script de forma muy sencilla y amigable. Una vez realizado, se copia y se pega en un editor de texto plano, se adiciona el código del comando que se quiere ejecutar y se asigna un nombre (en este caso script2.sh) junto con la extensión del lenguaje en que se ha escrito el script (en este caso bash, .sh). 

Una vez generado el script se lanza al backend, o  gestor de trabajos SLURM,  de la siguiente forma
```
sbatch script2.sh
```

Y automáticamente se genera un ID JOB

$Submitted batch job 25489521

Para más información acerca de las buenas prácticas y demás comandos para hacer seguimiento de los trabajos en los sistemas SLURM del NLHPC y Geryon, les recomendamos visitar las páginas anteriormente mencionadas y realizar los cursos de capacitación que ofrecen regularmente los administradores de estos servidores.
