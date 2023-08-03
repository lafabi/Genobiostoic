## Obtención de archivos  Binary Alingment Map BAM

Los archivos SAM obtenidos en el paso previo, son archivos pesados, más aun cuando trabajamos con genomas de alta cobertura. En tal sentido, nos conviene transformar éstos archivos SAM en archivos BAM (Binary Alingment Map). Para ello, ocupamos el programa *samtools* función *view*. Veremos que podemos comenzar a aplicar filtros particulares de aquí en adelante, por ejemplo relacionados con la calidad de mapeo contra el genoma de referencia o mantener sólo los reads que estén apropiadamente pareados en el mapeo. 


```
#!/bin/bash
#---------------Script SBATCH - NLHPC ----------------
#SBATCH -J Samtools-view
#SBATCH -p slims
#SBATCH --reservation=bioagosto
#SBATCH -n 5
#SBATCH -c 1
#SBATCH --mem-per-cpu=2300
#SBATCH --mail-user=email
#SBATCH --mail-type=ALL
#SBATCH -t 2:2:5
#SBATCH -o Samtools-view_%j.out
#SBATCH -e Samtools-view_%j.err

SAM=/home/courses/studentXX/genomes
BAM=/home/courses/studentXX/genomes

source $HOME/miniconda3/bin/activate
source activate assembly   

samtools view -q 10 -f 0x2 -bSh -@ 5 $SAM/m2267.sam > $BAM/m2267.bam 
```
## Ordenamos los reads mapeados

En el siguiente paso usamos el programa *samtools* de nuevo, esta vez con la función * sort*. Como su nombre lo indica, el *sort* se utiliza para ordenar un archivo de formato BAM. En ocasiones,las lecturas no siempre se almacenan en un orden específico y en este caso se debe editar el archivo con la finalidad de facilitar ciertas operaciones y además mejorar la eficiencia cuando se trabaja con los datos datos. El orden que vamos a otorgar a nuestros datos obedece al mismo lineamiento de coordenadas del genoma de referencia. Como vemos, la sintaxis de este script es muy sencilla, basta con indicar el archivo de entrada o *input*, que es el que obtuvimos previamnete con *samtools view* y generar un archivo de salida o *output* con los reads mapeados y ordenados según las coordenadas genómicas del genoma de referencia de Tasha.

```
#!/bin/bash
#---------------Script SBATCH - NLHPC ----------------
#SBATCH -J Samtools-sort
#SBATCH -p slims
#SBATCH --reservation=bioagosto
#SBATCH -n 5
#SBATCH -c 1
#SBATCH --mem-per-cpu=2300
#SBATCH --mail-user=email
#SBATCH --mail-type=ALL
#SBATCH -t 2:2:5
#SBATCH -o Samtools-sort_%j.out
#SBATCH -e Samtools-sort_%j.err

SORTBAM=/home/courses/studentXX/genomes
BAM=/home/courses/studentXX/genomes

source $HOME/miniconda3/bin/activate
source activate assembly   

samtools sort -o $SORTBAM/m2267.sorted.bam -@ 5 $BAM/m2267.bam

```

