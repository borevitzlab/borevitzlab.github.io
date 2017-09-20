
# Notes to ourselves

>  Tips, tricks and gotchas for our future selves.


# Reading BCFs in IGV

IGV will not take the bcf, and it will only take a vcf if it is gz compressed and if the file ending is vcf.gz.

```bash
bcftools view -Ov freebayes.bcf > freebayes.vcf
bgzip freebayes.vcf
tabix freebayes.vcf.gz
```


# Sorting a multi-fasta file by name

This is useful for when a reference genome does not come with chromosomes or contigs in a sensible order. The sorting order could be changed by modifying the `sort -n` below to suit.

```bash
samtools faidx file.fasta && \
samtools faidx file.fasta $(cut -f1 file.fasta.fai | sort -n) > file_sorted.fasta
```

