# Lateral-Gene-Transfer-from-endosymbiontic-Wolbachia-bacteria-into-host-genome-
Host is ancient asexual oribatid mite Platynothrus peltifer


1. Verification for parts of Woblachia genome integrated into Ppr. genome

- download genome of Folsomia endosymbiont Wolbachia from NCBI (accession number :ASM193175v2)

#### Blastn of Wolbachia endosymbiont of Folsomia genome against Ppr. genome 

Database für Blast :

In : makeblastdb  –in Ppr_instagrall.polished.FINAL.copy.fa  –dbtype nucl –parse_seqids 

Megablast/normales Format:
In : 

blastn -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2Einzeln_genomic.fna  -out normalesFormat_megablast_Fol

Out : Scratch/linda/Natalie/Genomes/Wolbachia/results/Fsm_megablast.results

Megablast/Outformat6:
In : 
blastn -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2Einzeln_genomic.fna  -outfmt "6 qseqid sseqid$
t length mismatch gapopen qstart qend sstart send evalue pident slen qcovs " -out Fsm_megablast6.results

Out : Scratch/linda/Natalie/Genomes/Wolbachia/results/Fsm_megablast6.results

Blastn/Outformat6 (auch entfernter ähnliche Hits finden)

In : 
blastn -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2Einzeln_genomic.fna -task blastn -num_threads 40 -outfmt 6 "qseqid sseqid piden
t length qstart qend sstart send slen qcovs" -out Fsm_blast6.results

Out : Scratch/linda/Natalie/Genomes/Wolbachia/results/Fsm_blast6.results
 
sorting/filtering results for length of blast hits and percentage identity : 

awk '$3 or $4 >= 150 {print $0}' Fsm_blast6.results (pident/length)

grep -w  "chr1“ Fsm_blast6.results > Chr1 and so on

Sort by location of the alignment : sort -k5/7 -n (for location on query or on Ppr)

Blastn Haplotypen :

makeblastdb -in /home/linda/Scratch/Natalie/hap1/output_scaffolds.fasta -parse_seqids - dbtype nucl (hap1)

makeblastdb -in /home/linda/Scratch/Natalie/hap2/output_scaffolds100.fasta -parse_seqids - dbtype nucl (hap2)

In: blastn -db /home/linda/Scratch/Natalie/hap1/output_scaffolds.fasta -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2_genomic.fna  -task blastn -outfmt "6 01931755.2_ASM193175v2Einzeln_genomic.fna -task blastn -num_threads 40 -outfmt 6 "qseqid sseqid pident length qstart qend sstart send slen " -out result_hap1
(blastn_hap1.sh)

In hap2 :  blastn -db /home/linda/Scratch/Natalie/hap2/output_scaffolds100.fasta  -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2_genomic.fna  -task blastn -outfmt "6 01931755.2_ASM193175v2Einzeln_genomic.fna -task blastn -num_threads 40 -outfmt 6 "qseqid sseqid pident length qstart qend sstart send slen " -out results_hap2
(blastn_hap2.sh)

Everything done before was also run with -max tar_seq 1 to filter out for possible multiple alignments and keep only the one best hit in such cases

(results : /home/linda/Scratch/Natalie/blast.results/blastmaxtarseq <> /home/linda/Scratch/Natalie/hap1 and /home/linda/Scratch/Natalie/hap2



tblastx : 

Due to computational constraints the genome was divided into smaller parts (1/10 of original length) with overlapping ends to avoid losing possible hits and information by cutting through codons before using tblastx 

In : Folsomnia10.fna -Folsomnia10j.fna (for exact parts see Excel-Sheet)

In : tblastx -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query Folsomnia10.fna  -num_threads 20 -outfmt 6 -out Folsomnia10_tblastx.results (for each part of Wolbachia genome)
 
Out : Folsomnia10_tblastx.results - Folsomnia10j_tblastx.results

Blastx :

In : makeblastdb – in Ppr.pep –dbtype prot –parse_seqids 

blastx -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2_genomic.fna -subject /home/linda/Scretch/Natalie Per.pep  -outfmt 6 -evalue 1e-50 
-out /home/linda/Scratch/Natalie/blast.results/blastxFolsomia

For Phylogenie 

38 genomes of Wolbachia on full genome level from NCBI (for list of accession numbers of utilized genomes view excel sheet on google drive)
  
Cat : *.fna > Wolbachiaquerys

In : blastn -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query /home/linda/Scratch/Natalie/Wolbachiaquerys -task blastn -max_target_seqs 1 -num_threads 40 -outfmt "6 qseqid sseqid piden lenght qstart qend sstart send" -out Wolbachiaquerys.results


