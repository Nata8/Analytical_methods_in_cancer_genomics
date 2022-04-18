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
+ **BCFTOOLS** is a set of utilities that manipulate variant calls in the Variant Call Format (VCF) and its binary counterpart BCF. <br />
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
"mpileup" - generates genotype likelihoods at each genomic position with coverage 
"call" - makes the actual calls
> OPTIONS
"--ploidy" - an optional column indicating ploidy
"-m" - tells the program to use the default calling method
"-v" - asks to output only variant sites
"-0" - selects the output format
"-b" - chooses output format - binary compressed BCF
```

**Variant annotation**

Variant annotation is used to help researchers filter and prioritise functionally important variants for
further study. There are several popular programs available for annotating variants. <br />
To my mind, the most user friendly is Variant Effect Predictor (VEP) with [website.](https://covid-19.ensembl.org/Tools/VEP) <br />
First, we need to extract and copy all variants: <br />
` bcftools view calls.bcf | cut -f 1-5 | grep -v "^#"` <br />
Then, the results can be visualized by website mentioned above and evaluated using [Covid lineage comparation](https://outbreak.info/compare-lineages).
We can use filter to visualize only S protein variants, because these variants are better examined.
The S protein variants are localized at cDNA positions - 200, 203-209, 284 and 424-433. Most likely it is an omikron variant. 

