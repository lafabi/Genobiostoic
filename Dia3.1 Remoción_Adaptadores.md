# Remoción de Adaptadores o Trimming

Tal como estudiamos en la clase de *Herramientas de Secuenciación* la secuenciación genómica implica la adición de adaptadores, secuencias cortas para unirlo a la plataforma de secuenciación, que deben eliminarse después para obtener secuencias "limpias". Los *barcodes* se agregan a cada muestra antes de la secuenciación para identificarlas en un solo análisis masivo.La mayoría de las plataformas de secuenciación eliminan los adaptadores o barcodes, sin embargo, en ocasiones podemos detectar restos de adaptadores en nuestros reads genómicos a travpes de los procesos de verificación de calidad tales como  ```fastqc```

En esta etapa del taller comenzaremos a editar y generar varios archivos de importancia para la resecuenciación genómica. Para ello comenzaremos a remover los adaptadores o secuencias sobrerrepresentadas que pueden quedar como remanentes de la plataforma de secuenciación de Ilumina. Para ello ocuparemos el programa ```Trimommatic```. Una vez ingresado en el servidor NLHPC a través de ```ssh``` muévase a su dierctorio /home/fleon/Genobiostoic/usuario. Paralelamente, abra el generador de scripts de la página del NLHPC https://wiki.nlhpc.cl/Generador_Scripts. Modifique sus parámetros de nombre de taeras, procesadores, memoria, etc.

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
ADAPT=/home/fleon/Adapt

source $HOME/miniconda3/bin/activate
source activate assembly   

trimmomatic PE -threads 10 -phred33 $GEN/m2267sub2_R1.fastq.gz $GEN/m2267sub2_R2.fastq.gz -baseout $TRIM/m2267.trim.fq ILLUMINACLIP:$ADAPT/TruSeq2OVR-PE.fa:2:30:10:1:true LEADING:3 TRAILING:3 MAXINFO:40:0.4 MINLEN:36

```

Una vez diseñado el script abrimos ``` nano ``` y escogemos un nombre alusivo a la función de este script, tal como *trimming.sh*. Seguidamente podemos enviarlo a correr al backend a través del siguiente comando: 

```
sbatch trimming.sh
```

En este punto, monitorizaremos dos cosas,1) la verificación de la corrida en el backend a través del comando ```squeue``` y 2) verificando que se generen los archivos de salidas en los directorios que redirigimos en la ruta del script.

Los archivos de salida de esta corrida tendrán 4 tipos de extensiones .1U, .2U, .1P, .2P, el prefijo de cada uno de estos archivos será el mismo del nombre de los genomas tal como los definimos en el script, en este caso particular *m2267*. Estas extensiones *U* y *P* se refieren a reads que están pareados *.P* y los que no están pareados *.U*.Recordemos que en el proceso de secuenciación se hacen lecturas en un sentido y otras en antisentido. De esta forma,tendremos reads o lecturas simples (sólo en un sentido) o lecturas pareadas (en un sentido y antsentido).

Una vez finalizado el proceso, tendremos listos nuestros archivos de salida para iniciar el segundo paso de alineamiento contra genoma el genoma de referencia escogido para los zorros, en este caso nuestro genoma de referencia es el Perro o *Canis lupus familiaris*. Para ello, ya hemos descargado el genoma de referencia ```GCF_000002285.5_Dog10K_Boxer_Tasha_genomic.fna```   en el directorio ```/home/fleon/genomes/Index```. Este genoma de referencia fue indexado a través del programa ```BWA-MEM``` y se generaron los archivos con las siguientes extensiones :  dog_index.amb  dog_index.ann  dog_index.bwt  dog_index.pac  dog_index.sa. 


> Para abarcar los objetivos de este taller, y cumplir con los tiempos decidimos tener generados estos archivos previamente

 El script para generar estos índices se muestra a continuación:

 
```
#!/bin/bash
#SBATCH -J Canis-index
#SBATCH -p general
#SBATCH -n 5
#SBATCH --mem-per-cpu=3000
#SBATCH -t 10:00:00
#SBATCH -o  Canis-index%j_%x.out
#SBATCH -e  Canis-index%j_%x.err

source /home/fleon/miniconda3/bin/activate
source activate assembly

REF=/home/fleon/genomes/Index

bwa index -p $REF/dog_index $REF/GCF_000002285.5_Dog10K_Boxer_Tasha_genomic.fna

```


El script lo puede guardar con el nombre alusivo a la función del su contenido

El script para generar estos indices se muestra a continuación, por temas de tiempo en este taller ya habíamos generado estos archivos

> + sinfo : muestra el estado de las particiones
> + squeue - u : muestra la cola de tareas
> + scancel : mata un trabajo
> + sbatch : corre un script en el backend
> + srun : corre un script en el frontend
> + sacct -X : muestra el estado de todas la tareas ejecutadas
> + scontrol -dd show job IDtrabajo: detalla la información del trabajo 
> + sstat : Dice la cantidad de recursos utilizados por un trabajo


