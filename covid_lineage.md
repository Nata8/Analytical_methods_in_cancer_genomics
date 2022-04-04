# SARS-Cov-2 Lineage Determination

Workflow for alignment of FASTQ files to the SARS-Cov-2 reference genome, calling and annonationing variants. Furthermore, determination of the most likely lineage. <br />
<br />
<br />
**Install all prerequisities** <br />

`sudo apt-get update` <br />
+ **SAMTOOLS** is a suite of programs for interacting with high-throughput sequencing data. <br />
`sudo apt install samtools` <br />
+ **BWA** is a software package for mapping low-divergent sequences against a large reference genome. <br />
`sudo apt install bwa` <br />

**Make a new directory and change the current working directory** <br />

`mkdir analytical_methods_in_cancer` <br />
`cd analytical_methods_in_cancer` <br />

**Download reference genome and FASTQ files** <br />

`wget https://gear.embl.de/data/.slides/Plate135H10.R2.fastq.gz`<br />
`wget https://gear.embl.de/data/.slides/Plate135H10.R2.fastq.gz` <br />

Fasta file with reference covid genome can be found [here.](https://www.ncbi.nlm.nih.gov/nuccore/NC_045512.2?report=fasta) <br />
`nano reference_covid.fasta` <br />

 
 **Index the reference genome**
 
 BWA first needs to construct FM-index for the reference genome. <br />
`bwa index reference_covid.fasta` <br />

**Make an alignment**

First part of the pipeline: BWA-MEM alghorithm performs local alignment. <br />
Second part of the pipeline: Sort the alignments by leftmost coordinates and write the result to the file align.bam. <br />
`bwa mem reference_covid.fasta Plate135H10.R1.fastq.gz Plate135H10.R2.fastq.gz | samtools sort -o align.bam -` <br />
Index the BAM file for fast random access. <br />
`samtools index align.bam` <br />
``
``
``
