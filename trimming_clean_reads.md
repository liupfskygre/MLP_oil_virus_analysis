##


##


##1st
```
# source /home/PTPE2/Software/miniconda3/bin/activate

# HX_Cm_T55_G6

#

cd /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads

screen -S trimming_reads

conda activate trim

trimmomatic PE -phred33 /home/PTPE2/Project/mlp_data_liupengfei/metaG/HX_Cm_T55_G6/KD55-21-6-17_FDME210267481-1r_1.clean.fq.gz /home/PTPE2/Project/mlp_data_liupengfei/metaG/HX_Cm_T55_G6/KD55-21-6-17_FDME210267481-1r_2.clean.fq.gz HX_Cm_T55_G6_trimmed_R1.fastq.gz HX_Cm_T55_G6_trimmed_U_R1.fastq.gz HX_Cm_T55_G6_trimmed_R2.fastq.gz HX_Cm_T55_G6_trimmed_U_R2.fastq.gz ILLUMINACLIP:/home/PTPE2/User/liupf/Projects_liupf/common_files/TruSeq3-PE.fa:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15 MINLEN:36 -threads 60


#assembly of HX_Cm_T55_G6, metaspades

screen -r trimming_reads

#/home/PTPE2/Software/SPAdes-3.15.3-Linux/bin/metaspades.py  -1 HX_Cm_T55_G6_trimmed_R1.fastq.gz -2 HX_Cm_T55_G6_trimmed_R2.fastq.gz -o ./HX_Cm_T55_G6_spades --only-assembler -t 60 -k 33,55,77,99,127 -m 800 &>HX_Cm_T55_G6_spades.log

/home/PTPE2/Software/SPAdes-3.15.3-Linux/bin/spades.py --meta  -1 HX_Cm_T55_G6_trimmed_R1.fastq.gz -2 HX_Cm_T55_G6_trimmed_R2.fastq.gz -o ./HX_Cm_T55_G6_spades --only-assembler -t 60 -k 33,55,77,99,127 -m 800 &>HX_Cm_T55_G6_spades.log
 cd HX_Cm_T55_G6_spades
 seqkit stats -a scaffolds.fasta
# file             format  type  num_seqs      sum_len  min_len  avg_len    max_len   Q1   Q2   Q3  sum_gap    N50  Q20(%)  Q30(%)
# scaffolds.fasta  FASTA   DNA    256,135  229,401,608      128    895.6  1,658,739  323  425  679        0  1,422       0       0



#test1, with different kmers
/home/PTPE2/Software/SPAdes-3.15.3-Linux/bin/spades.py --meta  -1 HX_Cm_T55_G6_trimmed_R1.fastq.gz -2 HX_Cm_T55_G6_trimmed_R2.fastq.gz -o ./HX_Cm_T55_G6_spades-2 --only-assembler -t 60 -k 21,33,55,77 -m 800 &>HX_Cm_T55_G6_spades-2.log
#file             format  type  num_seqs      sum_len  min_len  avg_len    max_len   Q1   Q2   Q3  sum_gap    N50  Q20(%)  Q30(%)
#scaffolds.fasta  FASTA   DNA    334,376  238,602,913       78    713.6  1,072,582  261  334  525        0  1,123       0       0



#test2, with megahit
megahit -1 HX_Cm_T55_G6_trimmed_R1.fastq.gz -2 HX_Cm_T55_G6_trimmed_R2.fastq.gz  --k-min 41 --k-max 121 --k-step 10 --mem-flag 2 -m 0.75 --out-prefix HX_Cm_T55_G6_megahit -t 60 --out-dir ./HX_Cm_T55_G6_megahit &> HX_Cm_T55_G6_megahit.log

stats.sh

#keep using the data from test1, -k 21, 33, 55,77
#10k data is similar, 25kb scaoffold is higher in test1 than test2
#megahit is not good

```

#trimm other metaG data

```
source /home/PTPE2/Software/miniconda3/bin/activate


/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scripts/trim_for_loop_run.sh trim_sample.tsv 6

nano /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scripts/trim_for_loop_run.sh

```


##trimming metaT reads
```
#### most rbisome RNA are remove during lib constructioin, sortmeRNA additonally remove 1.5% ribsome rRNA left

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scripts/trim_for_loop_run.sh trim_sample.tsv 4



```
