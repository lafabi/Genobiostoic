# Uso de Servidores de alta Capacidad


El uso de servidores remotos es cada vez más común y posibilita la oportunidad de ocupar, eficientemente, múltiples procesadores de alto rendimiento. Cada servidor tiene su propio tipo de configuración, arquitectura, capacidades, particiones y pueden tener o no agendadores de tareas o "*Schedulers*". Les sugerimos que a la hora de ocupar un servidor de alta capacidad, aprendan sobre su estructuración y funcionamiento a través de las instrucciones de sus administradores.
Una de las primeras tareas que debemos aprender para trabajar con servidores remotos es cómo conectarnos; para ello usamos el comando ```ssh``` (security shell). Este comando nos permite hacer una conexión segura desde la máquina local a la remota. Una vez abierta la cuenta en el servidor remoto, el administrador del servidor nos otorgará un usuario y un password. En muchas ocasiones necesitaremos una dirección IP para poder establecer la conexión:

Para usuarios de servidores de alta capacidad tal como el caso del NLHPC de la Universidad De Chile, nuestro usuario lucirá así: 

```studentXX@leftraru.nlhpc.cl```
``` passw: XXXX```

Para el caso particular de servidores remotos que no son de alta capacidad debemos contar con la dirección IP. En este caso el usuario lucirá de esta forma:
```usuario@146.155.227.140```
```passw: XXXX```

Para conectarnos basta colocar el comando ```ssh``` antes del usuario:

```
ssh studentXX@leftraru.nlhpc.cl

```
Inmediatamente el servidor nos solicitará el password.

```studentXX@146.155.227.140's password:```


En ocasiones, la primera vez que nos conectamos a un servidor remoto, éste nos solicita compartir una llave de seguridad para establecer una conexión segura de intercambio de archivos y transferencia de información, de esta forma puede aparecer un diálogo en pantalla y aceptaremos tipeando un *s*

Una vez conectado en el servidor, entraremos al *home* del usuario hospedero, que en este ejemplo es ```student98```. Al ingresar listaremos el contenido del directorio con ```ls``` y veremos el siguiente contenido: 

![Z.png](https://github.com/lafabi/Genobiostoic/blob/main/ejemplo_contenidodir.png)


Si utilizamos el comando ```pwd```, veremos que estamos ubicados en la carpeta /home/courses/studentXX. Dado que varios participantes están utilizando el mismo usuario, crearemos un directorio de scripts con el nombre de cada uno usando ```mkdir```. Verificamos que cada nombre del usuario escogido por participante se haya creado dentro de /home/courses/studentXX a través del comando ```ls```


Al igual que nuestra máquina local, éstos servidores ofrecen la alternativa de correr scripts en el **frontend**, pero no es la mejor opción, dado que se ocupan los recursos informaticos de forma poco eficiente. En este caso, los servidores de alta capacidad tales como el NLHPC de la Universidad de Chile [https://www.nlhpc.cl/](https://www.nlhpc.cl/) o [Geryon https://www3.astro.puc.cl/geryon/](https://www3.astro.puc.cl/geryon) de la Universidad Católica funcionan con un sistema de planificador de tareas o *Schedulers*. Este sistema opera asignando filas y prioridades a las tareas según la capacidad de los recursos, administrando de mejor forma los recursos tales como memoria, núcleos, tiempo de ejecución de trabajos, etc. Estos scripts se corren en el **backend**, que es un espacio donde se llevan a cabo tareas en el sistema operativo oculto de fondo. 
