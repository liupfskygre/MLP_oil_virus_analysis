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



```

#trimm others

```
source /home/PTPE2/Software/miniconda3/bin/activate


trim_for_loop_run.sh  6


```
