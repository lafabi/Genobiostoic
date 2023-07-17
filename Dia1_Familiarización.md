# Familiarización con la terminal bash: Día 1

**Qué es la terminal Bash o shell?**

La "shell" es una interfaz gráfica que opera a través de líneas de comando, éstos comandos son, de por sí, programas que actúan como interlocutores o intérpretes entre sistemas complejos y nosotros. Entre sus principales atributos destacan su capacidad de multitarea y multiusuario. La caracteristica multitarea, como su nombre lo indica, permite realizar más de una función o tarea simultáneamente en varias ventanas o pestañas. Por otra parte el rasgo multiusuario, permite realizar distintas tareas a más de una persona en la misma terminal simultánemente.

Como mencionamos con anterioridad, nos podemos comunicar con el sistema operativo a través de un interlocutor, los comandos. Ahora, comenzaremos a aprender un lenguaje que nos permitirá interactuar y dar instrucciones al sistema para la ejecución de una tarea. Usualmente, los comandos son acrónimos de palabras en inglés y se definen según la función que desempeñan.

Primero hagamos un saludo al sistema operativo y haremos que se imprima en la pantalla a través del comando ``echo`` (es un eco de lo que quieres imprimir en pantalla)

```
echo Hello World
```


## Navegar entre sistemas de archivos

Muchas veces nos resultará útil saber en qué carpeta estamos (desde ahora llamaremos a las carpetas directorios), para ello utilizamos el comando ``pwd`` (print working directory)

```
 pwd
```
```/home/fabiola```

Generalmente cuando ingresamos por primera vez a la terminal, el sistema nos redirige al home del usuario. Será conveniente cambiarnos de directorio y para ello usaremos el comando ``cd`` (change directory).

```
cd Documentos
```

Ahora verifiquemos que nos cambiamos de directorio con pwd

```
pwd
```
```/home/fabiola/Documentos```

Dado que nos cambiamos a Documentos, ahora creemos un subdirectorio dentro de Documentos con el comando ``mkdir`` (make directory).

```
mkdir Genobiostoic
```

Verifiquemos que se haya creado el ditectorio Genobiostoic a través del comando ``ls`` (list) 

```
ls
```

Aquí observamos que se ha creado un nuevo directorio llamado Genobiostoic,su directorio parental es Documentos. Verifiquemos el sistema anidado y jerarquico de directorios con ``pwd``

```
pwd
```
```/home/fabiola/Documentos/Genobiostoic```

En la terminal, las rutas relativas y absolutas se utilizan para especificar la ubicación de un archivo o directorio en el sistema de archivos. Una ruta absoluta, como su nombre lo indica, es una ruta completa que comienza desde la raíz o home  del sistema de archivos y especifica la ubicación exacta de un archivo o directorio, en linux toda ruta absoluta comienza con un slash (/). Por el contrario una ruta relativa especifica la ubicación de un archivo o directorio en relación con la ubicación actual. No comienza con un slash (/)  y depende la ruta donde se encuentre el usuario.


Ahora que tenemos creado un directorio llamado *Genobiostoic* construyamos esta jerarquía de archivos:

![Jerarquía de directorios](https://github.com/lafabi/Genobiostoic/blob/main/Jerarquia_Dir.png)



## Interactuar con archivos

Lo primero que haremos en esta sección será crear un archivo con un editor de texto. La terminal shell trae un editor de texto instalado llamado ``nano``. Basta con invocarlo tipeando nano en la terminal 

```
nano
```

A continuación se abre una ventana en la que podemos pegar, tipear y/o editar el texto que deseemos. Presionando ^x salimos del editor de texto nano y regresamos a la terminal. Ahora que sabemos invocar el editor de texto procedamos a crear un documento de texto plano .txt llamado verde. Para ello copiemos el poema de Federico García Lorca (Disponible al final de esta sección) y a continuación invoquemos ```nano``` y creemos al mismo tiempo el documento con su nombre y extensión:

```
nano verde.txt
```

Ahora peguemos el poema de Federico Garcia Lorca dentro del documento en nano, guardemos con ^o y salgamos de nano con ^x.Verifiquemos que se ha creado el documento con el comando ``ls``, debería aparecer el nombre del documento "verde.txt" en el directorio

```
ls
```

En este punto aprenderemos varios comandos que nos permitiran interactuar con estos archivos, como vimos el programa ```nano``` nos confiere el permiso de editar o modificar el documento, ahora bien, muchas veces queremos ver el documento, es decir imprimir el contenido en la pantalla sin que sea modificado. Para esto ocupamos el comando ``cat`` (concat):

```
cat verde.txt
```

A continuación el texto contenido en el documento se imprimirá en la pantalla. Muchas veces, cuando trabajamos con datos genómicos muy grandes es poco conveniente imprimir todo su contenido, de hecho la concatenación del documento puede durar varios minutos. Si nos pasa esto podemos detener la impresión en pantalla con ^C. Si deseamos limpiar la pantalla, basa con tipear clear en la terminal:

```
clear
```

Como mencionamos, en ocasiones queremos imprimir el encabezado o cierto número de líneas del documento, para ello utilizamos el comando ``head`` (head):

```
head verde.txt
```

Varios comandos tienen ciertas funciones, por ejemplo ``head`` acompañado de la función ``-n 40`` imprime en pantalla las primeras 40 lineas del documento:

```
head -n 40 verde.txt
```


También, podemos imprimir el final de un documento con el comando ``tail`` 

```
tail verde.txt
```

Al igual que ``head``, ``tail`` acepta la función ``-n`` y podemos imprimir las lineas que deseemos.


Cuando se trabajan con datos Genómicos, muchas veces queremos buscar, ubicar o filtrar ciertos loci, cromosomas, individuos etc dentro de un archivo, para ello ocupamos el comando ``grep`` (globally search for regular expression and print out). En este ejemplo buscaremos la palabra verde en el texto verde.txt, para ello tipearemos:

```
grep verde verde.txt
```

Aquí, vale la pena resaltar que dimos una instrucción distinta, ordenamos buscar (``grep``) una palabra (verde) en un archivo (verde.txt). De esta forma diseñamos la sintaxis de un programa un poco más complejo que los anteriores.

Ahora vayamos más allá y buquemos (``grep``) un palabra (Compadre) y contemos cuántas veces se repite con ``wc`` (word count)

```
grep Compadre verde.txt | wc -l
```


## Poema de Federico García Lorca *Romance Noctámbulo*

```

Verde que te quiero verde.

Verde viento. Verdes ramas.

El barco sobre la mar

y el caballo en la montaña.

Con la sombra en la cintura

ella sueña en su baranda

verde carne, pelo verde,

con ojos de fría plata.

Verde que te quiero verde.

Bajo la luna gitana,

las cosas la están mirando

y ella no puede mirarlas.

 

Verde que te quiero verde.

Grandes estrellas de escarcha,

vienen con el pez de sombra

que abre el camino del alba.

La higuera frota su viento

con la lija de sus ramas,

y el monte, gato garduño,

eriza sus pitas agrias.

¿Pero quién vendrá? ¿Y por dónde…?

Ella sigue en su baranda,

verde carne, pelo verde,

soñando en la mar amarga.

Compadre, quiero cambiar

mi caballo por su casa,

mi montura por su espejo,

mi cuchillo por su manta.

Compadre, vengo sangrando

desde los puertos de Cabra.

 

Si yo pudiera, mocito,

este trato se cerraba.

Pero yo ya no soy yo,

ni mi casa es ya mi casa.

Compadre, quiero morir

decentemente en mi cama.

De acero, si puede ser,

con las sábanas de holanda.

¿No veis la herida que tengo

desde el pecho a la garganta?

Trescientas rosas morenas

lleva tu pechera blanca.

Tu sangre rezuma y huele

alrededor de tu faja.

Pero yo ya no soy yo.

Ni mi casa es ya mi casa.

Dejadme subir al menos

hasta las altas barandas,

¡Dejadme subir!, dejadme

hasta las altas barandas.

Barandales de la luna

por donde retumba el agua.

 

Ya suben los dos compadres

hacia las altas barandas.

Dejando un rastro de sangre.

Dejando un rastro de lágrimas.

Temblaban en los tejados

farolillos de hojalata.

Mil panderos de cristal,

herían la madrugada.

 

Verde que te quiero verde,

verde viento, verdes ramas.

Los dos compadres subieron.

El largo viento dejaba

en la boca un raro gusto

de hiel, de menta y de albahaca.

¡Compadre! ¿Dónde está, dime?

¿Dónde está tu niña amarga?

¡Cuántas veces te esperó!

¡Cuántas veces te esperara,

cara fresca, negro pelo,

en esta verde baranda!

 

Sobre el rostro del aljibe,

se mecía la gitana.

Verde carne, pelo verde,

con ojos de fría plata.

Un carámbano de luna

la sostiene sobre el agua.

La noche se puso íntima

como una pequeña plaza.

Guardias civiles borrachos

en la puerta golpeaban.

Verde que te quiero verde.

Verde viento. Verdes ramas.

El barco sobre la mar.

Y el caballo en la montaña.

```
