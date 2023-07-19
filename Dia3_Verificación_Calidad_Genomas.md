# Verificación de Calidad de lo Genomas en el servidor NLHPC

Para verificar la calidad de los genomas, primero hay que recibirlos de la plataforma de secuenciación y luego subirlos a los servidores de alta capacidad. Supongamos que tenemos los sigueintes genomas de zorros
m2267sub2_R1.fastq.gz  m2267sub2_R2.fastq.gz  m2293sub2_R1.fastq.gz  m2293sub2_R2.fastq.gz contenidos en el directorio Zorros/ y los queremos subir al servidor del NLHPC con destino al directorio /home/fleon, ocuparemos el comando ```rsync``` junto con otros operadores de la siguiente forma:

```
rsync -azvrP -e Zorros/ ssh fleon@leftraru.nlhpc.cl:/home/fleon/ 

```

El comando ```rsync``` no solamente nos permite transferir archivos, sino que además nos verifica la imagen de integridad de la transferencia y si se llegara a intyerrumpir la conexión de transferencia, al volverlo a ejecutal comenzaría desde el punto donde se interrumpió y seguiría transfiriendo lo que resta de archivos.

En ocasiones, deberíamos verificar la imágen de intregridad o fidelidad de tranferencia  a travpes del comando ```md5sum``` éste crea unaimagen en caracteres alfa numéricos que debe coincidir con el archivo de origen, basa tipear:

```
md5sum  archivo.txt
```
La imagen  tardará en imprimirse dependiendo del tamaño del archivo. Esta imagen se corroborará con la imagen original de donde originalmente se haya realizado la descarga. En este caso si los archivos son copia fie y exacta recibiremos un mensaje comoÑ

```la imagen coinciden```

Una vez descargados los genomas de Zorros y verificado la imágenes correspondientes, procederemos a verificar la calidad de los genomas y para ello ocuparemos el programa ```FastQC```
para efectos de este taller estarán instalados los programas en el servidor, éstos estarán disponibles a través de ```conda```

Los genomas estarán depositados en el siguiente directorio ```/home/fleon/genomes/``. Es hora de elaborar nuestro primer Script: 


```
#!/bin/bash
#---------------Script SBATCH - NLHPC ----------------
#SBATCH -J FastQC-zorro
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
QC=/home/fleon/usuario/QC

source $HOME/miniconda3/bin/activate
conda activate assembly

fastqc -o $QC/ --noextract -t 1 -f fastq $GEN/*.gz


```

Verificaremos la ejecución en tiempo real de este proceso imprimiento el archivo FastQC_%j.out con el comando ```cat```

```
cat FastQC_%j.out

```

Aquí observaremos un diálogo que el proceso avanza en un 5, 10 y 15% prograsivamnete. Entre los comandos que nos permitirán hacer un seguimiento y comunicarnos con el backend tenemos los siguientes: 


Sinfo : muestra el estado de las particiones
Squeue - u : muestra la cola de tareas
Scancel : mata un trabajo
Sbatch : corre un script en el backend
Srun : corre un script en el frontend
Sacct -X : muestra el estado de todas la tareas ejecutadas
Scontrol -dd show job IDtrabajo: detalla la información del trabajo 
Sstat : Dice la cantidad de recursos utilizados por un trabajo

Una vez terminado la verificación de la calidad de los genomas, se creará en nuesto directorio  ```/home/fleon/genomes/QC``` archivos html
 y otros archivos .zip. A continuación realizaremos un resumen de estos análisis de calidad con el programa ``multiqc``. dado que este programa es muy rápido y no ocupa muchos recursos lo enviaremos a correr en el frontend del servidor de la siguiente forma:

```
source $HOME/miniconda3/bin/activate
multiqc QC/
```

Inmediatamente aparecerá un diálogo de la ejecución dl programa ``multiqc``

Al igual que ``fastqc`` se generará un archivo html que NO podremos visualizar en el servidor. de esta forma debemos descargarlo a la máquina local a través de este comando desde nuestra máquina local, es decir no desde el servidor:

```
rsync -azvrP -e  ssh fleon@leftraru.nlhpc.cl:/home/fleon/genomes/QC/multiqc.html ./

```
 Una vez descargado este archivo procederemos a abrirlo a través de su enlace a una pagina web. Aquí veremos un resumen de la calidad de los reads entregados por la empresa de secuenciación:

 + Cuántos millones de reads tenemos entre los R1 y R2?
 + Cuántas secuencias duplicadas tenemos?
 + Cuál es el tamaño promedio de los reads
 + Poseen restos de adaptadores?
 + Qué significan los colores verdes, amarillos y rojos en cada análisis?

 




