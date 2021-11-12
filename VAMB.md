
##
```
# https://github.com/RasmussenLab/vamb

```

#
##


#for each sample,
#
```

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads
source /home/PTPE2/Software/miniconda3/bin/activate
conda activate metabat2_vamb

screen -r checkM

cat mapping_template.txt |cut -f1 -d, > sample_list.txt
sh ./bam_cov_vamb.sh sample_list.txt 25

#./GD_bbmap_binning/GD_vamb/
```


#test one
#jgi depth needs to reformate
```
#formate

awk '
  FNR==NR{P[$1];next}
  FNR==1{
    for(i=1;i<=NF;i++) {
      c=$i
      sub(/\.[XYZ]$/,"",c)
      if(c in P)S[i]
    }
  }
  { a=x
    for(i=1;i<=NF;i++)
    if(!(i in S)) a=a " " $i;
    print substr(a,2)
  }' header_pattern.txt GD_megahit_full_depth.txt > GD_megahit_full_depth_vamb.txt


#Output format: contigName<tab>contigLen<tab>totalAvgDepth<tab>SAMPLE1.sort.bam<tab>Sample2.sort.bam<tab>...


vamb -o SEP --outdir GD_vamb --fasta ../GD.contigs_1.5kb.fa --jgi ./GD_megahit_full_depth.txt -p 20 -m 1500

vamb --outdir GD_vamb --fasta ../GD.contigs_1.5kb.fa --bamfiles *.bam -p 20 -m 1500

vamb.vambtools.write_bins

```


#test1
```
sh ./vamb_get_bins.sh try_vamb_id.txt

sh ./vamb_get_bins.sh sample_list_2.txt

```

#mv all *.fasta together
```
cd /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads/VAMB_MAGs


for file in $(cat sample_list.txt)
do
echo "${file}"

#for MAGs in ./"${file}"_bbmap_binning/"${file}"_vamb/*.fasta
#do
#mv "${MAGs}" ./VAMB_MAGs/
#done

ls ./"${file}"_bbmap_binning/"${file}"_vamb/*.fasta
ls ./"${file}"_bbmap_binning/"${file}"_vamb/*

done

#seqkit get the genome size
for file in *fasta
do
seqkit stats -j 20 -a ./"${file}" >> VAMB_MAGs_stats.txt
done

find -type f -name '*.fasta'  | wc -l

#keep only MAGs with 0.5Mb and larger

grep -v 'format' VAMB_MAGs_stats.txt >VAMB_MAGs_stats_noheader.txt


sed -e 's/,//g' VAMB_MAGs_stats_noheader.txt >VAMB_MAGs_stats_noheaderFx.txt

awk '$5>=1000000' VAMB_MAGs_stats_noheaderFx.txt >VAMB_MAGs_stats_noheader1M.txt
awk '$5>=500000' VAMB_MAGs_stats_noheaderFx.txt >VAMB_MAGs_stats_noheader05M.txt

#1443 VAMB_MAGs_stats_noheader1M.txt
#1809 VAMB_MAGs_stats_noheader05M.txt

cut -f1 -d$' ' VAMB_MAGs_stats_noheader05M.txt > VAMB_MAGs_stats_noheader05M_name.txt

sudo sed -i e 's/^\.//g' VAMB_MAGs_stats_noheader05M_name.txt

for file in $(cat VAMB_MAGs_stats_noheader05M_name.txt)
do
echo "${file}"
mv "${file}" /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/MLP_All_raw_MAGs/
done

```



##scripts

#get bins out
#vamb_get_bins.sh
```
#!/usr/bin/sh

#call sh ./vamb_get_bins.sh <sample_list>

depth=$1 #sample name

#cluster=$2 #cluster bin

#IFS=$'\n' #separate by "\n" for cat

for file in $(cat "${depth}")

do

cd ./"${file}"_bbmap_binning/"${file}"_vamb

sed -e 's/\t/,/g' clusters.tsv > cluster.fix.txt

cat cluster.fix.txt |cut -d, -f1 |sort|uniq > bin_id.txt

for line in $(cat bin_id.txt)
do
echo "${line}"

grep -w -e "${line}" clusters.tsv > bin.contig.txt

#ggrep -w -e '1' clusters.tsv > 1.bin.contig.txt

sed -e 's/\t/,/g' bin.contig.txt > bin.contig_fix.txt
#sed -e 's/\t/,/g' 1.bin.contig.txt >1.bin.contig_fix.txt

cat  bin.contig_fix.txt|cut -f2 -d, > bin_contigsID.txt
#cat  1.bin.contig_fix.txt|cut -f2 -d, > 1.bin_contigsID.txt


seqkit grep -j 20 -n -f bin_contigsID.txt ../../"${file}".contigs_1.5kb.fa -o "${file}"_vamb"${line}".fasta

#seqkit grep -n -f 1.bin_contigsID.txt ../../GD.contigs_1.5kb.fa -o GD_vamb_1.fasta


done

cd ../../
done

echo "finish all"

#unset IFS

```

#bam_cov_vamb.sh
```
#!/usr/bin/bash

#  bam_cov_vamb.sh
#
#
#  Created by Pengfei Liu on 1/15/21.
#

#call bam_cov_vamb.sh meta.data [threads]

depth=$1 #sample name

threads=$2

#check
echo "${depth}" "${threads}"

#
for file in $(cat "${depth}")

do

cd "${file}"_bbmap_binning

vamb --outdir "${file}"_vamb --fasta ../"${file}".contigs_1.5kb.fa --bamfiles *.bam -p 25 -m 1500

cd ..
done
#


```

#clean
```
for file in $(cat sample_list.txt)

do

cd "${file}"_bbmap_binning

rm "${file}"_megahit_full_depth.txt

rm -r "${file}"_metabat2

rm *megahit_metabat2.log
cd ..
done


```
