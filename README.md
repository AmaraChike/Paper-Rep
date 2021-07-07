# Paper-Rep
A reproduction of a paper as part of the requirements for Hackbio's bioinformatics fellowship




## Name of paper and link  


Repeated local emergence of carbapenem-resistant Acinetobacter baumannii in a single hospital ward   https://doi.org/10.1099/mgen.0.000050

## Sequence alignment
Illumina paired end sequences of Acinetobacter baumannii was gotten from the ENA website in fastq.gz format 



Study ascension number : ERP001080


Alignment was carried out using the bwa software  git@github.com:lh3/bwa.git

Install bwa

git clone https://github.com/lh3/bwa.git

command line bwa mem -t ref.idx read1.fq read2.fq > sample.sam
 
Creating reference index

Reference genome was gotten from  https://www.ncbi.nlm.nih.gov/nuccore/CP001921.1  GenBank accession number CP001921.1

command line bwa index ref.fasta index_prefix

Converting Sam to Bam


samtools sort sample.sam -o mysample.sorted.bam


The command can also be piped to save time

bwa mem ref.idx read1.fq read2.fq | samtools sort -o mysample.sorted.bam

## SNP identification

Freebayes v1.3.2 git@github.com:freebayes/freebayes.git


freebayes -f ref.fa aln.bam >var.vcf








