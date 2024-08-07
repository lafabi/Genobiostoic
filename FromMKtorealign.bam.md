
**¿Desde Marcar los duplicados hasta los archivos realign. ?**

```
picard MarkDuplicates I=$PATH/${sample}*_sorted.bam O=$PATH/${sample}*_sorted_dedup.bam METRICS_FILE=$PATH/${sample}*_sorted_dedup.metrics.txt VALIDATION_STRINGENCY=LENIENT CREATE_INDEX=true CREATE_MD5_FILE=true TAGGING_POLICY=All ASSUME_SORT_ORDER=coordinate
```

```
picard CreateSequenceDictionary -R $REF/GCA_010085355.fna --CREATE_MD5_FILE true -O $REF/GCA_010085355.dict --VALIDATION_STRINGENCY LENIENT --VERBOSITY ERROR
```

```
gatk3 -nt 6 -T RealignerTargetCreator -R $REF/GCA_010078495.1_BGI_Enov.V1_genomic.fna -I $PATH/${sample}_sorted_dedup.bam -o $PATH/${sample}.realn.intervals -allowPotentiallyMisencodedQuals -S LENIENT
```

```
gatk3 -T IndelRealigner -R $REF/index_Enovo_ref/GCA_010078495.fna -I $PATH/${sample}_sorted_dedup.bam -targetIntervals $PATH/${sample}.realn.intervals -o $PATH/${sample}.realign.bam -allowPotentiallyMisencodedQuals -S LENIENT --generate_md5 
```
