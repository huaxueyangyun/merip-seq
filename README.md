#exomePeak R
#Homo_sapiens.GRCh38.91.gtf from ensembl
args=commandArgs(T)
library("exomePeak")
gtf <- "/media/nbfs/nbCloud/public/nbcplatform/genome/index/PRICE/9606/GRCh38_Ensembl91/Homo_sapiens.GRCh38.91.gtf"
IP_BAM1=paste0(args[1],".sorted.bam")
IP_BAM2=paste0(args[2],".sorted.bam")
IP_BAM3=paste0(args[3],".sorted.bam")
INPUT_BAM1=paste0(args[4],".sorted.bam")
INPUT_BAM2=paste0(args[5],".sorted.bam")
INPUT_BAM3=paste0(args[6],".sorted.bam")
TREATED_IP_BAM1=paste0(args[7],".sorted.bam")
TREATED_IP_BAM2=paste0(args[8],".sorted.bam")
TREATED_IP_BAM3=paste0(args[9],".sorted.bam")
TREATED_INPUT_BAM1=paste0(args[10],".sorted.bam")
TREATED_INPUT_BAM2=paste0(args[11],".sorted.bam")
TREATED_INPUT_BAM3=paste0(args[12],".sorted.bam")
#comparison
exomepeak(GENE_ANNO_GTF=gtf, IP_BAM=c(IP_BAM1,IP_BAM2,IP_BAM3), INPUT_BAM=c(INPUT_BAM1,INPUT_BAM2,INPUT_BAM3),PEAK_CUTOFF_PVALUE=0.05,PEAK_CUTOFF_FDR=NA,FRAGMENT_LENGTH=200,
EXPERIMENT_NAME="ctrl")
exomepeak(GENE_ANNO_GTF=gtf, IP_BAM=c(TREATED_IP_BAM1,TREATED_IP_BAM2,TREATED_IP_BAM3), INPUT_BAM=c(TREATED_INPUT_BAM1,TREATED_INPUT_BAM2,TREATED_INPUT_BAM3),PEAK_CUTOFF_PVALUE=0.05,PEAK_CUTOFF_FDR=NA,FRAGMENT_LENGTH=200,
EXPERIMENT_NAME="treat")
exomepeak(GENE_ANNO_GTF=gtf, IP_BAM=c(IP_BAM1,IP_BAM2,IP_BAM3), INPUT_BAM=c(INPUT_BAM1,INPUT_BAM2,INPUT_BAM3),PEAK_CUTOFF_PVALUE=0.05,PEAK_CUTOFF_FDR=NA,FRAGMENT_LENGTH=200,
TREATED_IP_BAM=c(TREATED_IP_BAM1,TREATED_IP_BAM2,TREATED_IP_BAM3), TREATED_INPUT_BAM=c(TREATED_INPUT_BAM1,TREATED_INPUT_BAM2,TREATED_INPUT_BAM3),EXPERIMENT_NAME="diff")

warnings()
#homer
#Homo_sapiens.GRCh38.91.dna.primary_assembly.fa from ensembl
findMotifsGenome.pl peak.bed \
GRCh38_Ensembl91/Homo_sapiens.GRCh38.91.dna.primary_assembly.fa homer_out/ -len 6 -rna -p 20
