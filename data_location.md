##server PTPE2
```
IP:         172.21.83.54
系统版本    Ubuntu 20.04.2 LTS
账号密码：  user; PTPE2 —— LZU_ptpe2

ssh PTPE2@172.21.83.54
LZU_ptpe2

```

## common_files
```
/home/PTPE2/User/liupf/Projects_liupf/common_files/TruSeq3-PE.fa


```


##
```
/home/PTPE2/Project/mlp_data_liupengfei

# /Users/pengfeiliu/Biogas_institute/Projects_on_going/MLP厌氧培养体系病毒组/
############ ############ ############ metagenome_clean reads (not trimmed)
/home/PTPE2/Project/mlp_data_liupengfei/metaG

for file in $(ls -1)
do
echo ${file}
ls -1 $PWD/"${file}"/*.gz
done
```
############ ############ ############ metagenome trimmed reads
```
/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads

```

############ ############ ############ contigs
```
/Users/pengfeiliu/Biogas_institute/Projects_on_going/MLP厌氧培养体系病毒组

for file in $(ls -1)
do
echo ${file}
ls -1 $PWD/"${file}"/*scaffold*
done
```


############ ############ ############ metatranscriptomic clean reads (not trimmed)
```
for file in $(ls -1)
do
echo ${file}
ls -1 $PWD/"${file}"/*.gz
done

##all are done with sortmeRNA，only mRNA transcirpts left；
## most rbisome RNA are remove during lib constructioin, sortmeRNA additonally remove 1.5% ribsome rRNA left

```

############ ############ ############ metatranscriptomic trimmed reads
```
#


```

##work dir
```
/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus

#trimmed_reads
mkdir trimmed_reads

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads

zcat /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads/HX_O_T45_r1_trimmed_R1.fastq.gz /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads/HX_O_T45_r2_trimmed_R1.fastq.gz > HX_O_T45_r2_trimmed_CatR1.fastq.gz

zcat /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads/HX_O_T45_r1_trimmed_R2.fastq.gz /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads/HX_O_T45_r2_trimmed_R2.fastq.gz > HX_O_T45_r2_trimmed_CatR2.fastq.gz

#metaT_trim_reads
/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/metaT_trim_reads

```

#dReped MAGs
```
PTPE2@user-PowerEdge-R740:~/Project/mlp_data_liupengfei/derep_MAGs$ pwd
/home/PTPE2/Project/mlp_data_liupengfei/derep_MAGs

```

#####################################################PTPE3 #############################
```
# /home/PTPE3/User/liupf/liupf_projects_analysis/mlp_oil_virus




```
