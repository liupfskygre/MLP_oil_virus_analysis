##maxbin2

#for each sample,
#
```
#https://sourceforge.net/projects/maxbin2/files/

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads
source /home/PTPE2/Software/miniconda3/bin/activate
conda activate  maxbin2

screen -r checkM

cat mapping_template.txt |cut -f1 -d, > sample_list.txt
sh ./bam_cov_maxbin2.sh sample_list.txt 30

# [-min_contig_length (minimum contig length. Default 1000)]

```


#bam_cov_maxbin2.sh
```
#!/usr/bin/bash

#  bam_cov_maxbin2.sh
#
#
#  Created by Pengfei Liu on 1/15/21.
#

#call bam_cov_metabat2.sh meta.data [threads]

depth=$1 #sample name

threads=$2

#check
echo "${depth}" "${threads}"

#
for file in $(cat "${depth}")

do

cd "${file}"_bbmap_binning

if test -f abundance_list.txt
then
echo "abundance file exists"

else
echo "abundance file  not found"
for line in *.bam
do
/home/PTPE2/Software/bbmap/pileup.sh in="${line}"  out="${line%.*}"_cov.txt #

awk '{print $1"\t"$2}' "${line%.*}"_cov.txt | grep -v '^#' > "${line%.*}"_abundance.txt #should be $2 (Ave_fold)

done

ls -1 *_abundance.txt > abundance_list.txt

fi


mkdir "${file}"_maxbin2

run_MaxBin.pl -thread "${threads}" -contig ../"${file}".contigs_1.5kb.fa -out ./"${file}"_maxbin2/"${file}"_mxb -abund_list abundance_list.txt
cd ..
done
#
```

#clean
```
for file in *_bbmap_binning
do
cd "${file}"
rm -r  *_maxbin2
rm *_cov.txt
rm abundance_list.txt
rm *_abundance.txt
cd ..
done
```


```
mkdir maxbin2_M1C1D5_idba
cd maxbin2_M1C1D5_idba

screen -S maxbin2_M1C1D5_idba

#abundance file, if you have stats from bbmaping,no need of pileup.sh for cov cal
pileup.sh in=Aug_M1_C1_D5_idba_random.sam  out=cov.txt #idental to  Aug_M1_C1_D5_idba_random.stats

awk '{print $1"\t"$2}' cov.txt | grep -v '^#' > abundance.txt #should be $2 (Ave_fold)

# Aug_M1_C1_D5_idba_random.stats

/opt/MaxBin-2.2.4/run_MaxBin.pl -thread 40 -contig scaffold.fa -out idba_k60_maxbin2 -abund abundance.txt


```
