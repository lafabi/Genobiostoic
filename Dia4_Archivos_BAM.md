## Obtención de archivos  Binary Alingment Map BAM

```
#!/bin/bash
#---------------Script SBATCH - NLHPC ----------------
#SBATCH -J Samtools-view
#SBATCH -p general
#SBATCH -n 5
#SBATCH -c 1
#SBATCH --mem-per-cpu=4250
#SBATCH --mail-user=email
#SBATCH --mail-type=ALL
#SBATCH -t 2:2:5
#SBATCH -o Samtools-view_%j.out
#SBATCH -e Samtools-view_%j.err

SAM=/home/fleon/genomes/
BAM=/home/fleon/genomes/

source $HOME/miniconda3/bin/activate
source activate assembly   

samtools view -q 10 -f 0x2 -bSh -@ 5 $SAM/m2267.sam > $BAM/m2267.bam 
```

```
#!/bin/bash
#---------------Script SBATCH - NLHPC ----------------
#SBATCH -J Samtools-sort
#SBATCH -p general
#SBATCH -n 5
#SBATCH -c 1
#SBATCH --mem-per-cpu=4250
#SBATCH --mail-user=email
#SBATCH --mail-type=ALL
#SBATCH -t 2:2:5
#SBATCH -o Samtools-sort_%j.out
#SBATCH -e Samtools-sort_%j.err

SORTBAM=/home/fleon/genomes/
BAM=/home/fleon/genomes/

source $HOME/miniconda3/bin/activate
source activate assembly   

samtools sort -o $SORTBAM/m2267.sorted.bam -@ 40 $BAM/m2267.bam

```

