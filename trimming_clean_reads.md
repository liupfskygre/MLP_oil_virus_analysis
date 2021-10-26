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

```

#trimm others

```
source /home/PTPE2/Software/miniconda3/bin/activate


/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scripts/trim_for_loop_run.sh trim_sample.tsv 6

nano /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scripts/trim_for_loop_run.sh

```
