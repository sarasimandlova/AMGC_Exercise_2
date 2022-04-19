## Data preparation 

I first downloaded the necessary datasets:

`wget https://gear.embl.de/data/.exercise/tu.r1.fq.gz`

`wget https://gear.embl.de/data/.exercise/tu.r2.fq.gz`

`wget https://gear.embl.de/data/.exercise/wt.r1.fq.gz`

`wget https://gear.embl.de/data/.exercise/wt.r2.fq.gz`


`wget https://hgdownload.soe.ucsc.edu/goldenPath/hg19/bigZips/hg19.fa.gz`


I indexed the reference as follows: 

`bwa index hg19.fa.gz` 

## Align to the reference

`bwa mem hg19.fa.gz tu.r1.fq.gz tu.r2.fq.gz | samtools sort -o atu.bam - `

`bwa mem hg19.fa.gz wt.r1.fq.gz wt.r2.fq.gz | samtools sort -o awt.bam - `

I Indexed the BAM file as follows: 

`samtools index atu.bam`

`samtools index awt.bam`

## Region of interest

Subsetting the BAM to the region of interest: 

`samtools view -b atu.bam chrX:20000000-40000000 > roi_tu.bam `

`samtools view -b awt.bam chrX:20000000-40000000 > roi_wt.bam `

## Read depth
I used `samtools depth` to found out the coverage:

`samtools depth roi_tu.bam > tu.output`

`samtools depth roi_wt.bam > wt.output`

## Read depth plot


