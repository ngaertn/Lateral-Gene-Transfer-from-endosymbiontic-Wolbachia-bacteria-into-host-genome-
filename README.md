# Lateral-Gene-Transfer-from-endosymbiontic-Wolbachia-bacteria-into-host-genome-
Host is ancient asexual oribatid mite Platynothrus peltifer


1. Verification for parts of Woblachia genome integrated into Ppr. genome

- download genome of Folsomia endosymbiont Wolbachia from NCBI 

- Blastn of Wolbachia endosymbiont of Folsomia genome against Ppr. genome 

Database für Blast :

In : makeblastdb  –in Ppr_instagrall.polished.FINAL.copy.fa  –dbtype nucl –parse_seqids 

Megablast/normales Format:
In : 
blastn -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2Einzeln_genomic.fna  -out Fsm_megablast.results
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
 
Sortieren/Filtern Ergebnisse : 
awk '$3 >= 150 {print $0}' Fsm_blast6.results
grep -w  "chr1“ Fsm_blast6.results > Chr1 usw 
Sortieren nach Lage der Blast-Hits mit sort -k5/7 -n 

Blastn Haplotypen :
makeblastdb -in /home/linda/Scratch/Natalie/hap1/output_scaffolds.fasta -parse_seqids - dbtype nucl (hap1)
makeblastdb -in /home/linda/Scratch/Natalie/hap2/output_scaffolds100.fasta -parse_seqids - dbtype nucl (hap2)

In: blastn -db /home/linda/Scratch/Natalie/hap1/output_scaffolds.fasta -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2_genomic.fna  -task blastn -outfmt "6 01931755.2_ASM193175v2Einzeln_genomic.fna -task blastn -num_threads 40 -outfmt 6 "qseqid sseqid pident length qstart qend sstart send slen " -out result_hap1
(blastn_hap1.sh)

In hap2 :  blastn -db /home/linda/Scratch/Natalie/hap2/output_scaffolds100.fasta  -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2_genomic.fna  -task blastn -outfmt "6 01931755.2_ASM193175v2Einzeln_genomic.fna -task blastn -num_threads 40 -outfmt 6 "qseqid sseqid pident length qstart qend sstart send slen " -out results_hap2
(blastn_hap2.sh)

Everything noted above also done with -max tar_seq 1 to filter out for possible multiple alignments and keep only one best hit in such cases


tblastx : 
Due to computational constraints the genome was divided into smaller parts (1/10 of original length) with overlapping ends to avoid losing possible hits and information by cutting through codons before using tblastx 
In : Folsomnia10.fna -Folsomnia10j.fna (genaue Unterteilung der Abschnitte siehe Excel-Sheet)
Tblastx :
 In : tblastx -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query Folsomnia10.fna  -num_threads 20 -outfmt 6 -out Folsomnia10_tblastx.results (usw)
Out : Folsomnia10_tblastx.results - Folsomnia10j_tblastx.results

Blastx :
In : makeblastdb – in Ppr.pep –dbtype prot –parse_seqids 
blastx -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2_genomic.fna -subject /home/linda/Scretch/Natalie Per.pep  -outfmt 6 -evalue 1e-50 
-out /home/linda/Scratch/Natalie/blast.results/blastxFolsomia

Für Phylogenie 
38 Genome von Wb auf full genome level von NCBI/ exact 
Cat : *.fna > Wolbachiaquerys
In : blastn -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query /home/linda/Scratch/Natalie/Wolbachiaquerys -task blastn -max_target_seqs 1 -num_threads 40 -outfmt "6 qseqid sseqid piden lenght qstart qend sstart send" -out Wolbachiaquerys.results
Out : Wolbachiaquerys.results 
blastn -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2Einzeln_genomic.fna -task blastn -num_threads 30 -outfmt "6 qseqid sseqid pident length qstart qend sstart send evalue bitscore" -out Fsm_blast6.results
