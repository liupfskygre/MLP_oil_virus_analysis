##

#
```
screen -S checkV-all

checkv end_to_end MLP_oil10kscaf_virus_can.fasta MLP_oil_checkv_out -t 30 -d /home/PTPE2/Software/biodatabase/checkv_db/checkv-db-v1.0

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scaffolds10k/virus_calling_out/MLP_oil_checkv_out


#统一病毒名称,再次跑checkv，避免一个contigs出现两个provirous带来的名称统一
cat proviruses.fna viruses.fna > virus_tmp.fasta

sed -i -e 's/ .*$//g' virus_tmp.fasta
sed -i -e 's/_1$//g' virus_tmp.fasta #

#rerun checkV
#
checkv end_to_end virus_tmp.fasta virus_tmp_checkv_output_directory -t 30 -d /home/dell/biodb/checkv-db-v1.0



#discarded list

##keep blank derived vOTUs to remove see what are they and remove contaminations

#
grep -e 'blank' quality_summary.tsv > quality_summary1_blank.tsv
#1167 blanks

#among them, xxx are with 0 virus genes and with >=1 host genes,
##these need to be discardeded number
#virus gene==0 and host gene>=1
awk '$6==0&&$7>0' quality_summary.tsv |wc -l
#1359

awk '$6==0&&$7>0' quality_summary.tsv | cut -f1 -d$'\t' > EV_virus_discarded_seq.txt
#1359

#kept
seqkit grep -n -v -f EV_virus_discarded_seq.txt  ../virus_tmp.fasta -o EV_virus_final.fasta

seqkit stats EV_virus_final.fasta

file                  format  type  num_seqs      sum_len  min_len   avg_len    max_len
EV_virus_final.fasta  FASTA   DNA      4,282  169,214,163    1,257  39,517.6  1,298,124

#remove sequence w lenght <5000 bp after trimming

#before xxx

cat EV_virus_final.fasta | seqkit seq -m 5000 -g | seqkit stats
# 4243 sequences


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
