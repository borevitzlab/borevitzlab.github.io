
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
FASTA_TO_SORT=somefile.fasta

# Check if the fasta file has been indexed already, if not, index it
test -f ${FASTA_TO_SORT}.fai || samtools faidx ${FASTA_TO_SORT})

# Grab out the sequences by name in the correct order.
samtools faidx ${FASTA_TO_SORT} $(cut -f1 ${FASTA_TO_SORT}.fai | sort -n) > file_sorted.fasta
```

The beauty of this is that it uses very little RAM even on huge references, as it uses `samtools faidx` to perform random access into the fasta file.
