# Remoción de Adaptadores o Trimming

Tal como estudiamos en la clase de *Herramientas de Secuenciación* la secuenciación genómica implica la adición de adaptadores, secuencias cortas para unirlo a la plataforma de secuenciación, que deben eliminarse después para obtener secuencias "limpias". Los *barcodes* se agregan a cada muestra antes de la secuenciación para identificarlas en un solo análisis masivo.La mayoría de las plataformas de secuenciación eliminan los adaptadores o barcodes, sin embargo, en ocasiones podemos detectar restos de adaptadores en nuestros reads genómicos a travpes de los procesos de verificación de calidad tales como  ```fastqc```

En esta etapa del taller comenzaremos a editar y generar varios archivos de importancia para la resecuenciación genómica. Para ello comenzaremos a remover los adaptadores que pueden quedar como remanentes de la plataforma de secuenciación de Ilumina. Para ello ocuparemos el programa ```Trimommatic```. Una vez ingresado en el servidor NLHPC a través de ```ssh``` muévase a su dierctorio /home/fleon/Genobiostoic/usuario. Paralelamente, abra el generador de scripts de la página del NLHPC https://wiki.nlhpc.cl/Generador_Scripts. Modifique sus parámetros de nombre de taeras, procesadores, memoria, etc.

```
#!/bin/bash
#---------------Script SBATCH - NLHPC ----------------
#SBATCH -J Trimmomatic
#SBATCH -p general
#SBATCH -n 5
#SBATCH -c 1
#SBATCH --mem-per-cpu=4250
#SBATCH --mail-user=email
#SBATCH --mail-type=ALL
#SBATCH -t 2-2:2:5
#SBATCH -o Trimmomatic_%j.out
#SBATCH -e Trimmomatic_%j.err


GEN=/home/fleon/genomes/
TRIM=/home/fleon/genomes/
ADAPT=/home/fleon/fabi/

source $HOME/miniconda3/bin/activate
conda activate assembly




 
source $HOME/miniconda3/bin/activate
source activate assembly   

trimmomatic PE -threads 10 -phred33 $GEN/${i}_R1.fastq.gz $GEN/${i}_R2.fastq.gz -baseout $TRIM/${i}.trim.fq ILLUMINACLIP:$ADAPT/TruSeq2OVR-PE.fa:2:30:10:1:true LEADING:3 TRAILING:3 MAXINFO:40:0.4 MINLEN:36

done


```
