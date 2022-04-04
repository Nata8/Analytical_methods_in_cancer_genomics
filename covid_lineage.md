# SARS-Cov-2 Lineage Determination

Workflow for alignment of FASTQ files to the SARS-Cov-2 reference genome, calling and annonationing variants. Furthermore, determination the most likely lineage. <br />
<br />
<br />
**Install all prerequisities** <br />

`sudo apt-get update` <br />
`sudo apt install samtools` <br />
`sudo apt install bwa` <br />

**Make a new directory and change the current working directory** <br />

`mkdir analytical_methods_in_cancer` <br />
`cd analytical_methods_in_cancer` <br />

**Download reference genome and FASTQ files** <br />

`wget https://gear.embl.de/data/.slides/Plate135H10.R2.fastq.gz`<br />
`wget https://gear.embl.de/data/.slides/Plate135H10.R2.fastq.gz` <br />

Fasta file with reference covid genome can be found [here](https://www.ncbi.nlm.nih.gov/nuccore/NC_045512.2?report=fasta)
`nano reference_covid.fasta` <br />

 
 **Index the reference genome**
 
 BWA first needs to construct FM-index for the refence genome. <br />
`bwa index reference_covid.fasta` <br />

**Make an alignment**

``
``
``
``
``
