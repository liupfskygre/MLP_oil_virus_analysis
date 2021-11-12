##

#
```
screen -S checkV-all

checkv end_to_end MLP_oil10kscaf_virus_can.fasta MLP_oil_checkv_out -t 30 -d /home/PTPE2/Software/biodatabase/checkv_db/checkv-db-v1.0

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scaffolds10k/virus_calling_out/MLP_oil_checkv_out

###
#discarded list
#among them, xxx are with 0 virus genes and with >=1 host genes,
##these need to be discardeded number
#virus gene==0 and host gene>=1
awk '$6==0&&$7>0' quality_summary.tsv |wc -l
#2591

awk '$6==0&&$7>0' quality_summary.tsv | cut -f1 -d$'\t' > MLP_virus_discarded_seq.txt

cat proviruses.fna viruses.fna > virus_tmp.fasta
#7424

sed -i -e 's/ .*$//g' virus_tmp.fasta
sed -i -e 's/_1$//g' virus_tmp.fasta

#kept
seqkit grep -n -v -f MLP_virus_discarded_seq.txt   virus_tmp.fasta -o MLP_total_virus_final1.fasta
#
/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scaffolds10k/virus_calling_out/MLP_oil_checkv_out/MLP_total_virus_final1.fasta
#4833

grep '>' MLP_total_virus_final1.fasta > MLP_total_virus_final1_seq.txt
sed -i -e 's/>//g' MLP_total_virus_final1_seq.txt

grep -w -f MLP_total_virus_final1_seq.txt quality_summary.tsv  > MLP_total_virus_final1_quality_summary.tsv
head -1 quality_summary.tsv > header_quality_summary.txt
cat header_quality_summary.txt MLP_total_virus_final1_quality_summary.tsv > MLP_total_virus_final1_quality_summaryH.tsv

#not used
#keep completeness larger than 10%， most of undetermined removed
#awk '$10>10&&$10!=NA' MLP_total_virus_final1_quality_summaryH.tsv | cut -f1 -d$'\t' > MLP_total_virus_final1_keep.tsv


```


#ref
```
作者在bitbucket上的建议是viral genes >= 5*host genes；这个阈值会不会过于严格了https://bitbucket.org/berkeleylab/checkv/issues/38/recommended-cutoffs-for-analyzing-checkv
Stephen Nayfach
Hey Josh - good to hear from you!

I would primarily use Virsorter2 for viral detection. But you can do an additional step to remove chromosome and plasmid contigs using the CheckV filter: viral_genes == 0 & host_genes > 0 & prophage == No. If you want to be more strict, you can keep only sequences where: viral_genes > 0 & viral_genes >= 5*host_genes, but I’d guess Virsorter identified most of these.

As far as completeness, I mainly focus on contigs with at least 50% completeness (high-quality or medium-quality in the quality_summary.tsv file). There may be some longer, clearly viral contigs w/o a good completeness estimate. You may or may not want to include those longer than a certain length (e.g. 20 Kb).
```
