# e_coli-example
steps from class to help annotate RNA-Seq data

/e_coli>ls
analysis  raw_data

~/e_coli>cd raw_data/
~/e_coli/raw_data>ls
DRR021342_1.fastq
DRR021342_2.fastq
GCF_000005845.2_ASM584v2_genomic.fna
GCF_000005845.2_ASM584v2_genomic.fna.amb
GCF_000005845.2_ASM584v2_genomic.fna.ann
GCF_000005845.2_ASM584v2_genomic.fna.bwt
GCF_000005845.2_ASM584v2_genomic.fna.fai
GCF_000005845.2_ASM584v2_genomic.fna.pac
GCF_000005845.2_ASM584v2_genomic.fna.sa
GCF_000005845.2.genes.gff
GCF_000005845.2.repeats.gff
NC_000913.3
SRR4342154_1.fastq
SRR4342154_2.fastq

~/e_coli>ls
analysis  raw_data
~/e_coli>cd analysis/
~/e_coli/analysis>ls
1_fastqc       3_fastqc  5_samtools  7_abyss
2_trimmomatic  4_bwa     6_snpEff    8_quast

~/e_coli/analysis>cd 1_fastqc/
~/e_coli/analysis/1_fastqc>ls
DRR021342_1_fastqc.html  DRR021342_2_fastqc.html
DRR021342_1_fastqc.zip   DRR021342_2_fastqc.zip

~/e_coli/analysis>cd 2_trimmomatic/
~/e_coli/analysis/2_trimmomatic>ls
DRR021342_1.trimmed.paired.fastq    DRR021342_2.trimmed.paired.fastq
DRR021342_1.trimmed.unpaired.fastq  DRR021342_2.trimmed.unpaired.fastq

trimmomatic PE \
../../raw_data/WTair2_S2_R1_001.fastq \
WTair2_S2_R1_001.trimmed.paired.fastq \
WTair2_S2_R1_001.trimmed.unpaired.fastq \
ILLUMINACLIP:/data/apps/trimmomatic/0.36/adapters/TruSeq3-PE.fa:2:30:10 \
SLIDINGWINDOW:4:15 MINLEN:75

#$ -N trim
#$ -q medium*
#$ -cwd
#$ -pe threads 8
java -Xmx4G -jar /lustre/projects/rnaseq_ws/apps/Trimmomatic-0.32/trimmomatic-0.32.jar \
SE \
-threads 8 \
-trimlog Filename.log \
-phred33 \
../../raw_data/ WTair2_S2_R1_001.fastq \
WTair2_S2_R1_001.trimmed.paired.fastq \
WTair2_S2_R1_001.trimmed.unpaired.fastq \
ILLUMINACLIP:/lustre/projects/staton/software/Trimmomatic-0.32/adapters/illuminaClipping.fa:2:30:10 \
SLIDINGWINDOW:4:15 MINLEN:75
>& trim.output

