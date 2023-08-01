# Uso de conda

Conda es un gestor de paquetes, dependencias y ambientes, que permite instalar programas evitando los conflictos entre distintas versiones de un mismo software. Por ejemplo, si tengo dos programas, digamos excel y powerpoint, y cada uno necesita la libería FONTS, pero excel la requiere en la versión 1.0, mientras que powerpoint requiere la versión 1.5.
Si tenemos ambos programas instalados sin separar ambientes, las dependencias entre si entrarán en conflicto, porque ambos programas piden distintas versiones.
Entonces, para tener ambas versiones instaladas para cada programa, se necesita separar los ambientes.

De esta forma, utilizaremos Conda para instalar programas para el análisis de datos biológicos.
La instalación de conda se puede ver en esta página:

```
https://docs.conda.io/projects/conda/en/latest/user-guide/install/linux.html
```

Nosotros ya lo tenemos instalado para cada usuario. Exploremos de qué trata.
Primero hay que activar conda

```
source ~/miniconda3/bin/activate
```

Veremos que aparece al lado izquierdo del prompt dice "(base)". Esto es porque se activó conda, y está en el ambiente base del programa, es decir, el ambiente principal.

Veamos qué paquetes tiene instalado:

```
conda list
```

Luego podemos ver qué ambientes existen:

```
conda info --envs
```

podemos activar el ambiente que tenemos instalado

```
conda activate assembly
```

y podemos ver qué programas tiene instalado con conda list, y luego desactivar el ambiente con 

```
conda deactivate
```


Vamos a crear nuestro propio ambiente. Para esto, tenemos que asignar un nombre (para las personas que compartan usuario, agreguen ***_nombre***), el canal desde donde se obtendrá la información de descarga de los paquetes, y el nombre del paquete.
Para verificar la calidad de los genomas, trabajaremos con fastQC:

```
conda create -n fastqc_nombre -c bioconda fastqc
```

No olviden reemplazar ***nombre*** por su nombre. Luego nos informará de lo que se está instalando, y nos pedirá aceptar (y) o rechazar (n). Aceptamos tecleando "y" y "enter".

Ahora que está creado el ambiente, lo activamos,  y luego vemos qué configuración nos permite hacer.

```
fastqc --help
```
