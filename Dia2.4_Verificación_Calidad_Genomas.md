# Verificación de calidad de reads en el servidor NLHPC

Para verificar la calidad de los genomas, primero hay que recibirlos de la plataforma de secuenciación y luego subirlos a los servidores de alta capacidad. Existen varias formas de transferir los archivos al servidor, que se mencionarán a continuación. Supongamos que tenemos los siguientes genomas de zorros, m2267sub2_R1.fastq.gz, m2267sub2_R2.fastq.gz, m2293sub2_R1.fastq.gz y m2293sub2_R2.fastq.gz contenidos un directorio de nuestra máquina local, y los queremos subir al servidor remoto del NLHPC con destino al directorio /home/fleon/genomes. Para realizar esta tarea, ocuparemos el comando ```rsync``` junto con otros operadores de la siguiente forma:

```
rsync -azvrP -e Zorros/ ssh fleon@leftraru.nlhpc.cl:/home/fleon/ 

```

>**Nota**: El comando, bajo el formato en el que está descrito, debe ejecutarse desde la carpeta Zorros, contenida en la máquina local. A grandes rasgos, el comando está indicando que se transifera todo lo contenido en la carpeta Zorros hacia la carpeta fleon, presente en el servidor remoto.

Al trabajar con datos genómicos, muchas veces grandes en peso y también numerosos, conviene estar atentos a que las transferencias se hagan de forma correcta, es decir que los archivos no estén *truncados*. Para ello, el comando ```rsync``` no solamente nos permite transferir archivos, sino que además nos verifica la imagen de integridad de la transferencia. De esta forma, si se llegara a interrumpir la conexión de transferencia, se recupera la información ya transferida al ejecutar el mismo comando otra vez, continuando la transferencia de datos desde el punto donde se interrumpió.

Ya una vez transferidos los genomas de Zorros al servidor (esto ya lo hemos hecho para ahorar tiempo), pasaremos al primer "análsis", que es comprobar la calidad de los genomas. Para ello ocuparemos el programa ```FastQC```, que para efectos de este taller ya está instalado en el servidor a través del gestor de paquetes llamado ```conda```.

Los genomas estarán depositados en el siguiente directorio ```/home/fleon/genomes/``. Crearemos un directorio dentro de nuestro usuario denominado QC/. Con esto, ya estamos listos para construir nuestro primer Script y enviarlo a través del *scheduler* SLURM al backend: 

```
#!/bin/bash
#---------------Script SBATCH - NLHPC ----------------
#SBATCH -J FastQC-tunombre
#SBATCH -p general
#SBATCH -n 1
#SBATCH -c 1
#SBATCH --mem-per-cpu=1500
#SBATCH --mail-user=email
#SBATCH --mail-type=ALL
#SBATCH -t 2:2:5
#SBATCH -o FastQC_%j.out
#SBATCH -e FastQC_%j.err

GEN=/home/fleon/genomes/
QC=/home/fleon/usuarios/tunombre/QC

source $HOME/miniconda3/bin/activate
conda activate assembly

fastqc -o $QC/ --noextract -t 1 -f fastq $GEN/*.gz


```
Verificaremos la ejecución en tiempo real de este proceso imprimiento el archivo FastQC_%j.out con el comando ```cat```

```
cat FastQC_%j.out

```

Aquí observaremos un diálogo que indica que el proceso avanza en un 5, 10 y 15% progresivamente. Entre los comandos que nos permitirán hacer un seguimiento y comunicarnos con el backend tenemos los siguientes: 


+ sinfo : Muestra el estado de las particiones.
+ squeue - u : Muestra la cola de tareas.
+ scancel : Mata un trabajo.
+ sbatch : Corre un script en el backend.
+ srun : Corre un script en el frontend.
+ sacct -X : Muestra el estado de todas la tareas ejecutadas.
+ scontrol -dd show job IDtrabajo: Detalla la información de un trabajo. 
+ sstat : Dice la cantidad de recursos utilizados por un trabajo.

Una vez terminado la verificación de la calidad de los genomas, se creará en nuesto directorio  ```/home/fleon/usuarios/tunombre/QC``` archivos html y otros archivos .zip. A continuación, realizaremos un resumen de estos análisis de calidad con el programa ``multiqc``, que también se encuentra instalado en el servidor. Dado que este programa es muy rápido y no ocupa muchos recursos, lo enviaremos a correr en el frontend del servidor de la siguiente forma:

```
source $HOME/miniconda3/bin/activate
multiqc QC/
```

Inmediatamente aparecerá un diálogo de la ejecución del programa ``multiqc``

Al igual que ``fastqc``, se generará un archivo html que NO podremos visualizar en el servidor, de forma que debemos descargarlo a la máquina local a través del siguiente comando. Para ello nos ubicamos en el directorio de la maquina local Genobiostoic/Terminal/Practica2 y ejecutamos este comando:

```
rsync -azvrP -e  ssh fleon@leftraru.nlhpc.cl:/home/fleon/genomes/usuarios/tunombre/multiqc.html ./

```
 Una vez descargado este archivo procederemos a abrirlo a través de su enlace a una pagina web. Aquí veremos un resumen de la calidad de los reads entregados por la empresa de secuenciación:

 + ¿Cuántos millones de reads tenemos entre los R1 y R2?
 + ¿Cuántas secuencias duplicadas tenemos?
 + ¿Cuál es el tamaño promedio de los reads
 + ¿Poseen restos de adaptadores?
 + ¿Qué significan los colores verdes, amarillos y rojos en cada análisis?







>En ocasiones, deberíamos verificar la imágen de intregridad o fidelidad de tranferencia de un archivo a través del comando ```md5sum```, éste crea una imagen en caracteres alfa numéricos que debe coincidir con el archivo de origen, basta tipear:
```
md5sum archivo.txt
```
>La imagen  tardará en imprimirse dependiendo del tamaño del archivo. Esta imagen se corroborará con la imagen original de donde originalmente se haya realizado la descarga. En este caso si los archivos son copia fiel y exacta recibiremos un mensaje como:
```la imagen coincide```
 




