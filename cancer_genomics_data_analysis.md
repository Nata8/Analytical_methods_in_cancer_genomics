# Analysis of cancer genomics sample

Exercise for analysis cancer genomics sample (a paired tumor-control sample set). This is a simulated Medulloblastoma sample with a matched control. 
The main objective of this exercise is to align the data to [the human reference genome.](https://hgdownload.soe.ucsc.edu/goldenPath/hg19/bigZips/hg19.fa.gz), to sort and index the alignments and to generate a read-depth plot. More info [here.](https://tobiasrausch.com/courses/cg/).

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

**Focus on the region of interest**

In order to save computing time, we are only focusing on chromosome X, concrete from 20Mbp to 40Mbp.  <br />
`samtools view -b <<input bam>> chrX:20000000-40000000 > <<filename of output bam>>`  <br />

**Finding read depth**

We can simply use Samtools to find out read counts.  <br />
`samtools depth <<input bam>> > <<output txt file>>` <br />
The result is a text file with three columns. First column indicates chromosome, second shows positions at the chromosome and third are the individual depths. <br />

**Read depth plot** <br />
<br />
Let's make the last step. We cannot forget that we have two samples - tumor and control, therefore we need two plots. <br />
Graphs can be plotted using Gnuplot tool. <br />
`gnuplot> set term png` <br />
`gnutplot> set output 'graph.png'` <br />
`gnuplot> plot '<<input txt>>' using 2:3 with lines` <br />
`gnuplot> exit` <br />

<br />

**X-axis represents chromosome position and Y-axis represents read dept.** <br />
<br />
**Read depth plot from tumor sample**<br />
<br />
![Graph](https://github.com/Nata8/Analytical_methods_in_cancer_genomics/blob/main/tumor_graph.png) <br />
<br />
<br />
**Read depth plot from control sample** <br />
<br />
![Graph](https://github.com/Nata8/Analytical_methods_in_cancer_genomics/blob/main/control_graph.png) <br />
<br />
<br />
**Read depth plot using windows of 10 000 bp** <br />.

`seq 2000 4000 | awk '{print "chrX\t"$1*10000"\t"($1+1)*10000"\tID"NR;}' > regions.bed` <br />
`samtools bedcov regions.bed opravnyalignment.bam | awk '{print $1"\t"$2"\t"$3"\t"$5/10000;}' > tu.bed` <br />
<br />
`> library(ggplot2)` <br />
`> data = read.table("tu.bed")` <br />
`> colnames(data) = c("chr", "start", "end", "cov")` <br />
`> myplot <- ggplot(data=data, aes(x=start, y=cov)) + geom_point()` <br />
`> pdf("ggplot.pdf")` <br />
`> print(myplot)` <br />
`> dev.off() ` <br />
