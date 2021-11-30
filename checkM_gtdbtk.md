##

## wkdir
```
PTPE2

cd ~/User/liupf/Projects_liupf/mlp_oil_virus/

mkdir MLP_All_raw_MAGs


/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs

```


#move all MAGs from metabat2, maxbin2, vamb together(0.5Mb)
```
cd /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads

for file in $(cat sample_list.txt)
do
echo "${file}"
mv "${file}"_bbmap_binning/"${file}"_metabat2/*.fa /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs/
mv "${file}"_bbmap_binning/"${file}"_maxbin2/*.fasta /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs/
done

#ls *.fa|wc -l,  2634
#ls *.fasta|wc -l,  2218
#ls *vamb*|wc -l,  1809
cd /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs/

#6661


#change fa to fasta
rename 's/\.fa$/\.fasta/' *.fa


#copy 479 representatives to all contigs

cp /home/PTPE2/Project/mlp_data_liupengfei/derep_MAGs/*.fa /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs/
#499

seqkit stats -j 20 -a *.fa > dReped499_stats.txt

sed -i -e 's/,//g' dReped499_stats.txt
awk '$5>=500000' dReped499_stats.txt|wc -l
#487

rename 's/\.fa$/\.fasta/' *.fa

#7160 MAGs
```


##checkM and gtdbtk
```
#checkM 检查MAG质量
#PTPE2
/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scripts/run_checkm.sh mlp_all_bins fasta ./ ./mlp_all_bins_checkm_output



#gtdbtk=========》 on PTPE1, running
/home/PTPE1/User/liupf/Projects_liupf/mlp_oil_virus_project/scripts/run_checkm.sh mlp_all_bins fasta ./ ./mlp_all_bins_checkm_output
#参数信息
#[输出表格] [MAG后缀-fa] [MAGs_存放路径] [输出结果目录]
/home/PTPE1/User/liupf/Projects_liupf/mlp_oil_virus_project/scripts/run_checkm.sh mlp_all_bins2 fasta ./ ./mlp_all_bins_checkm_output2


#gtdbtk=========》 on PTPE1, failed on first step ???
/home/PTPE1/User/liupf/Projects_liupf/mlp_oil_virus_project/scripts/run_gtdbtk.sh mlp_all_bins
gtdbtk classify_wf -x fasta --prefix mlp_all_bins --genome_dir ./ --out_dir gtdbtk_out --min_perc_aa 30 --cpus 60

#
#PTPE2
#copy gtdbtk_out to PTPE2

sudo find /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs/gtdbtk_out/ -type d -exec chmod 777 {} \;

#sudo find /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs/gtdbtk_out/ -type f -exec chmod 777 {} \;

gtdbtk classify_wf -x fasta --prefix mlp_all_bins --genome_dir ./ --out_dir gtdbtk_out --min_perc_aa 30 --cpus 10

#参数信息
#[输出表格前缀]


##合并表格
cd /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs
python3 /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scripts/add_gtdbtk_tax_to_checkm.py mlp_all_bins_checkm_summary.txt gtdbtk_out/mlp_all_bins.bac120.summary.tsv gtdbtk_out/mlp_all_bins.ar122.summary.tsv > ../mlp_all_bins._checkm_gtdbtk_summary.txt

cd /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/

```


```
[2021-11-12 22:47:37] INFO: GTDB-Tk v1.7.0
[2021-11-12 22:47:37] INFO: gtdbtk classify_wf -x fasta --prefix mlp_all_bins --genome_dir ./ --out_dir gtdbtk_out --min_perc_aa 30 --cpus 10
[2021-11-12 22:47:37] INFO: Using GTDB-Tk reference data version r202: /home/PTPE2/.conda/envs/gtdbtk/share/gtdbtk-1.7.0/db/
[2021-11-12 22:47:37] INFO: Identifying markers in 7,160 genomes with 10 threads.
[2021-11-12 22:47:37] TASK: Running Prodigal V2.6.3 to identify genes.
[2021-11-12 22:48:17] INFO: Completed 7,160 genomes in 39.48 seconds (181.37 genomes/second).
[2021-11-12 22:48:17] WARNING: Prodigal skipped 7158 genomes due to pre-existing data, see warnings.log
[2021-11-12 22:48:17] TASK: Identifying TIGRFAM protein families.
[2021-11-12 22:48:47] INFO: Completed 7,160 genomes in 29.91 seconds (239.42 genomes/second).
[2021-11-12 22:48:47] WARNING: TIGRFAM skipped 7,149 genomes due to pre-existing data, see warnings.log
[2021-11-12 22:48:47] TASK: Identifying Pfam protein families.
[2021-11-12 22:48:51] INFO: Completed 7,160 genomes in 3.71 seconds (1,931.14 genomes/second).
[2021-11-12 22:48:51] WARNING: Pfam skipped 7,149 genomes due to pre-existing data, see warnings.log
[2021-11-12 22:48:51] INFO: Annotations done using HMMER 3.3.2 (Nov 2020).
[2021-11-12 22:48:51] TASK: Summarising identified marker genes.
[2021-11-12 22:59:50] INFO: Completed 7,160 genomes in 10.97 minutes (652.41 genomes/minute).
[2021-11-12 22:59:53] INFO: Done.
[2021-11-12 22:59:55] INFO: Aligning markers in 7,160 genomes with 10 CPUs.
[2021-11-12 22:59:55] INFO: Processing 5,858 genomes identified as bacterial.
[2021-11-12 23:00:13] INFO: Read concatenated alignment for 45,555 GTDB genomes.
[2021-11-12 23:00:13] TASK: Generating concatenated alignment for each marker.
[2021-11-12 23:01:01] INFO: Completed 5,858 genomes in 43.62 seconds (134.29 genomes/second).
[2021-11-12 23:01:06] TASK: Aligning 120 identified markers using hmmalign 3.3.2 (Nov 2020).
[2021-11-12 23:33:59] INFO: Completed 120 markers in 32.83 minutes (3.66 markers/minute).
[2021-11-12 23:34:03] TASK: Masking columns of bacterial multiple sequence alignment using canonical mask.
[2021-11-12 23:40:21] INFO: Completed 51,358 sequences in 6.30 minutes (8,150.80 sequences/minute).
[2021-11-12 23:40:22] INFO: Masked bacterial alignment from 41,084 to 5,037 AAs.
[2021-11-12 23:40:22] INFO: 986 bacterial user genomes have amino acids in <30.0% of columns in filtered MSA.
[2021-11-12 23:40:23] INFO: Creating concatenated alignment for 50,372 bacterial GTDB and user genomes.
[2021-11-12 23:40:25] INFO: Creating concatenated alignment for 4,817 bacterial user genomes.
[2021-11-12 23:40:25] INFO: Processing 1,302 genomes identified as archaeal.
[2021-11-12 23:40:25] INFO: Read concatenated alignment for 2,339 GTDB genomes.
[2021-11-12 23:40:26] TASK: Generating concatenated alignment for each marker.
[2021-11-12 23:40:38] INFO: Completed 1,302 genomes in 9.55 seconds (136.32 genomes/second).
[2021-11-12 23:40:40] TASK: Aligning 122 identified markers using hmmalign 3.3.2 (Nov 2020).
[2021-11-12 23:47:12] INFO: Completed 122 markers in 6.48 minutes (18.81 markers/minute).
[2021-11-12 23:47:14] TASK: Masking columns of archaeal multiple sequence alignment using canonical mask.
[2021-11-12 23:47:41] INFO: Completed 3,641 sequences in 26.97 seconds (135.02 sequences/second).
[2021-11-12 23:47:41] INFO: Masked archaeal alignment from 32,754 to 5,124 AAs.
[2021-11-12 23:47:41] INFO: 211 archaeal user genomes have amino acids in <30.0% of columns in filtered MSA.
[2021-11-12 23:47:41] INFO: Creating concatenated alignment for 3,430 archaeal GTDB and user genomes.
[2021-11-12 23:47:41] INFO: Creating concatenated alignment for 1,091 archaeal user genomes.
[2021-11-12 23:47:41] INFO: Done.
[2021-11-12 23:47:46] TASK: Placing 1,091 archaeal genomes into reference tree with pplacer using 10 CPUs (be patient).
[2021-11-12 23:47:47] INFO: pplacer version: v1.1.alpha19-0-g807f6f3
[2021-11-13 00:26:29] INFO: Calculating RED values based on reference tree.
[2021-11-13 00:26:33] TASK: Traversing tree to determine classification method.
[2021-11-13 00:26:33] INFO: Completed 1,091 genomes in 0.58 seconds (1,888.12 genomes/second).
[2021-11-13 00:26:34] TASK: Calculating average nucleotide identity using FastANI (v1.32).
[2021-11-13 00:59:22] INFO: Completed 8,242 comparisons in 32.76 minutes (251.56 comparisons/minute).
[2021-11-13 00:59:25] INFO: 513 genome(s) have been classified using FastANI and pplacer.
[2021-11-13 00:59:27] TASK: Placing 4,817 bacterial genomes into reference tree with pplacer using 10 CPUs (be patient).
[2021-11-13 00:59:28] INFO: pplacer version: v1.1.alpha19-0-g807f6f3

```
