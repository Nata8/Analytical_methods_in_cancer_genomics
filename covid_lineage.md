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
+ **BCFTOOLS** is a set of utilities that manipulate variant calls in the Variant Call Format (VCF) and its binary counterpart BCF. 
`sudo apt install bcftools` <br />

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

`bwa mem reference_covid.fasta Plate135H10.R1.fastq.gz Plate135H10.R2.fastq.gz | samtools sort -o align.bam -` <br />
Index the BAM file for fast random access. <br />
`samtools index align.bam` <br />
```
BWA-MEM algorithm performs local alignment.
Samtools sort sorts the alignments by leftmost coordinates and write the result to the file align.bam.
```

**Variant calling**

BCFtools can be used for variant calling - the process of identifying differences between the reference genome and the samples
that have been sequenced. <br />
`bcftools mpileup -f reference_covid.fasta align.bam | bcftools call --ploidy 1 -mv -Ob -o calls.bcf` <br />
```
"mpileup" - multi-way pileup producing genotype likelihoods 
"call" - 
> OPTIONS
"--ploidy" - an optional column indicating ploidy
"-m" - 
"-v" -
"-0" - assume genotypes at missing sites are 0/0
"-b" - 

```

``
``
