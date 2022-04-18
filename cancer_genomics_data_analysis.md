# Analysis of cancer genomics sample



**Index the reference genome**
 
 BWA first needs to construct FM-index for the reference genome. <br />
`bwa index <<reference genome>>` <br />

**Make an alignment**

`bwa mem <<reference genome>> <<first read>> <<second read>> | samtools sort -o align.bam -` <br />
Index the BAM file for fast random access. <br />
`samtools index align.bam` <br />
```
BWA-MEM algorithm performs local alignment.
Samtools sort sorts the alignments by leftmost coordinates and write the result to the file align.bam.
```
