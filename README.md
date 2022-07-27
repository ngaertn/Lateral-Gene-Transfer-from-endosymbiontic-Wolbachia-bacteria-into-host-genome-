# Lateral-Gene-Transfer-from-endosymbiontic-Wolbachia-bacteria-into-host-genome-
Host is ancient asexual oribatid mite Platynothrus peltifer


1. Verification for parts of Woblachia genome integrated into Ppr. genome
- download genome of Folsomia endosymbiont Wolbachia from NCBI
- Blastn of Wolbachia endosymbiont of Folsomia genome against Ppr. genome 

blastn -db /home/linda/Scratch/Natalie/Ppr_instagrall.polished.FINAL.copy.fa -query /home/linda/Scratch/Natalie/GCF_001931755.2_ASM193175v2Einzeln_genomic.fna -task blastn -num_threads 30 -outfmt "6 qseqid sseqid pident length qstart qend sstart send evalue bitscore" -out Fsm_blast6.results
