# Paper-Reproduction
A reproduction of a paper as part of the requirements for Hackbio's bioinformatics fellowship




## Name of paper and link  


Repeated local emergence of carbapenem-resistant Acinetobacter baumannii in a single hospital ward   https://doi.org/10.1099/mgen.0.000050

## Sequence alignment
Illumina paired end sequences of Acinetobacter baumannii was gotten from the ENA website in fastq.gz format 



Study ascension number : ERP001080


Alignment was carried out using the bwa software  git@github.com/lh3/bwa.git

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



## SNP identification and filtering 


Freebayes v1.3.2 git@github.com:freebayes/freebayes.git


freebayes -f ref.fa mysample.sorted.bam > results.vcf


The VCF result is filtered using vcffilter, this command is piped 



freebayes -f ref.fa mysample.sorted.bam | vcffilter -f "QUAL > 33" >results.vcf





## Merging vcf results

Firstly, zip the vcf files 

bgzip results.vcf > results.vcf.gz

After zipping the files, they are indexed

tabix -p results.vcf.gz 


merging with bcftools


bcftools merge /path/to/all/files/to/be/merged > nameoffile.vcf


## Converting vcf file format to fasta

This was done using vcf2phylip  https://github.com/edgardomortiz/vcf2phylip


install vcf2phylip 

git clone https://github.com/edgardomortiz/vcf2phylip


python vcf2phylip.py -i nameoffile.vcf -f


## Phylogenetic tree

The phylogenetic tree was created with Mega-X https://www.megasoftware.net/



## Resistance Analysis

Ariba was used for this analysis https://github.com/sanger-pathogens/ariba

install ariba


pip3 install ariba


Download species data from PubMLST

ariba pubmlstget 'Acinetobacter baumannii' out


Run resistance analysis


ariba run out/ref_db reads_1.fq reads_2.fq out_dir


Get summary for all samples run


ariba summary out /path/to/all/resistance/reports 


   
			
			










