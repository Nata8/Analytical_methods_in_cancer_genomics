# SARS-Cov-2 Lineage Determination

Workflow for alignment of FASTQ files to the SARS-Cov-2 reference genome, calling and annonationing variants. Furthermore, determination the most likely lineage. <br />
<br />
<br />
<br />
**Install all prerequisities**
`sudo apt-get update`
`sudo apt install samtools`
`sudo apt install bwa`

**Make a new directory and change the current working directory** <br />

`mkdir analytical_methods_in_cancer` <br />
`cd analytical_methods_in_cancer` <br />

**Download reference genome and FASTQ files**

`wget https://gear.embl.de/data/.slides/Plate135H10.R2.fastq.gz`
`wget https://gear.embl.de/data/.slides/Plate135H10.R2.fastq.gz`
`nano reference_covid.fasta`
 
``
