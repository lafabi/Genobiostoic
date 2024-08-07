
**Desde Marcar los duplicados hasta los archivos realign**

## Marcar los duplicados con Picard
```
picard MarkDuplicates I=$PATH/${sample}*_sorted.bam O=$PATH/${sample}*_sorted_dedup.bam METRICS_FILE=$PATH/${sample}*_sorted_dedup.metrics.txt VALIDATION_STRINGENCY=LENIENT CREATE_INDEX=true CREATE_MD5_FILE=true TAGGING_POLICY=All ASSUME_SORT_ORDER=coordinate
```
## la obtención de los realign.bam consta de tres pasos

### La primera, e independiente de los otros procesos, es crear un tipo de índice .dict del genoma de referencia para el programa GATK

```
picard CreateSequenceDictionary -R $REF/GCA_010085355.fna --CREATE_MD5_FILE true -O $REF/GCA_010085355.dict --VALIDATION_STRINGENCY LENIENT --VERBOSITY ERROR
```
### El segundo paso, es obtener los intervalos de los indels a lo largo del genoma para luego hacer lo realineamientos
```
gatk3 -nt 6 -T RealignerTargetCreator -R $REF/GCA_010078495.1_BGI_Enov.V1_genomic.fna -I $PATH/${sample}_sorted_dedup.bam -o $PATH/${sample}.realn.intervals -allowPotentiallyMisencodedQuals -S LENIENT
```

### En el segundo paso se realiza el realineamiento como tal, en esta etapa GATK ocupa los intervalos calculados en el paso anterior para hacer realineamientos locales alrededor de los indels y mejorar la calidad de mapeo. La finalidad es dismunuir la probabilidad de hacer falsos llamados de variantes cuando se obtiene el archivo Variant Calling File o VCF.

```
gatk3 -T IndelRealigner -R $REF/index_Enovo_ref/GCA_010078495.fna -I $PATH/${sample}_sorted_dedup.bam -targetIntervals $PATH/${sample}.realn.intervals -o $PATH/${sample}.realign.bam -allowPotentiallyMisencodedQuals -S LENIENT --generate_md5 
```
