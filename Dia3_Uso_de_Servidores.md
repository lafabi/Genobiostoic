# Uso de Servidores de alta Capacidad


3)El uso de servidores remotos, es cada vez más común y posibilita la oportunidad de ocupar, eficientemente, múltiples procesadores de alto rendimiento. Cada servidor tiene su propio tipo de configuración, arquitectura, capacidades, particiones y pueden tener o no agendadores de tareas o Schedulers. Les sugerimos que , a la hora de ocupar un servidor de lata capacidad, aprendan sobre su estructuración y funcuonamiento a través de las instrucciones de sus administradores.
Una de las primeras taeras que debemos aprender para trabajar con servidores remotos es cómo conectarnos, para ello usamos el comando ```ssh``` (security shell), este comando nos permite hacer una conexión segura desde la máquina local a la remota, muchas veces entregando una llave de seguridad entre el usuario (nosotros) y el servidor remoto, aquí una imala entrega de esta lalve de seguridad al ingresar por primera vez a un servidor remoto:

![Key-print.png](https://github.com/lafabi/Genobiostoic/blob/main/Key-print.png)

Al igual que nuestra máquina local, éstos servidores ofrecen la alternativa de correr scripts en el frontend, pero no es la mejor alternativa, dado que se ocupan los recursos informaticos de forma poco eficiente. En este caso, los servidores de alta capacidad tales como el NLHPC de la Universidad de Chile [https://www.nlhpc.cl/](https://www.nlhpc.cl/) o [Geryon https://www3.astro.puc.cl/geryon/](https://www3.astro.puc.cl/geryon) de la Universidad Católica funcionan con un sistema de planificador de tareas. Este sistema opera asignando filas y prioridades a las tareas según la capacidad de los recursos, administrando de mejor forma los recursos tales como memoria, núcleos, tiempo de ejecución de trabajos, etc. Estos scripts se corren en el backend, que es un espacio donde se llevan a cabo tareas en el sistema operativo oculto de fondo. En el próximo apartado hablaremos con más detalle de este sistema de administrador de trabajos. Por ahora veremos la arquitectura en la construcción de estos scripts: 

Al igual que una carta, los scripts que se envían al backend tienen un "membrete" con una serie de intrucciones para el asistente "virtual", en ésta indicarán ciertas características de la tarea. 

Un detalle importante para tener en cuenta a la hora de construir un script es que deben ser construidos en editores de texto plano,tales como nano,vim, gedit,notepad, entre otros. No se deben realizar scripts en programas de editor de texto con formato tipo word, pues los diferentes tipos de formatos (margen,sangría,tipo de letras, etc) serán reconocidos erróneamente por los programas. 

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



Dependendiendo de los recursos que requiera el trabajo (nodos, hilos, memoria, tiempo), se escoje la partición en el servidor y se agrega la información necesaria para construir el "membrete" del script de forma muy sencilla y amigable.Una vez realizado se copia y se pega en un editor de texto plano, se adiciona el código comando que se quiere ejecutar y se asigna un nombre (e este caso script2.sh) junto con la extensión del lenguaje en que se ha escrito el script (en este caso bash, .sh). 

Una vez generado el script se lanza al backend, o  gestor de trabajos SLURM,  de la siguiente forma
```
$sbatch script2.sh
```

Y automáticamente se genera un ID JOB

$Submitted batch job 25489521
