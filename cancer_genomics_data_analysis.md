# Analysis of cancer genomics sample

Exercise for analysis cancer genomics sample (a paired tumor-control sample set). This is a simulated Medulloblastoma sample with a matched control. 
The main objective of this exercise is to align the data to the human reference genome (https://hgdownload.soe.ucsc.edu/goldenPath/hg19/bigZips/hg19.fa.gz), to sort and index the alignments and to generate a read-depth plot. More info. (https://tobiasrausch.com/courses/cg/)

**Index the reference genome**
 
 BWA first needs to construct FM-index for the reference genome. <br />
`bwa index <<reference genome>>` <br />

**Make an alignment**

`bwa mem <<reference genome>> <<first fasta file>> <<second fasta file>> | samtools sort -o align.bam -` <br />
Index the BAM file for fast random access. <br />
`samtools index align.bam` <br />
```
BWA-MEM algorithm performs local alignment.
Samtools sort sorts the alignments by leftmost coordinates and write the result to the file align.bam.
```
