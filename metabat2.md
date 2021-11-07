##


#for each sample,
#
```

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads
source /home/PTPE2/Software/miniconda3/bin/activate
conda activate metabat2_vamb

screen -r checkM

cat mapping_template.txt |cut -f1 -d, > sample_list.txt
sh ./bam_cov_metabat2.sh sample_list.txt 30

```


#bam_cov_metabat2.sh
```
#!/usr/bin/bash

#  bam_cov_metabat2.sh
#
#
#  Created by Pengfei Liu on 1/15/21.
#

#call bam_cov_metabat2.sh.sh meta.data [threads]

depth=$1 #sample name

threads=$2

#check
echo "${depth}" "${threads}"

#
for file in $(cat "${depth}")

do

cd "${file}"_bbmap_binning

#export OMP_NUM_THREADS=1 #normal it will take the core simliar to the number of samples

if test -f "${file}"_megahit_full_depth.txt
then
echo ""${file}"_megahit_full_depth.txt exists"

else
echo ""${file}"_megahit_full_depth.txt File not found"
jgi_summarize_bam_contig_depths --outputDepth "${file}"_megahit_full_depth.txt *bam.sorted
fi

rm -r "${file}"_metabat2
mkdir "${file}"_metabat2

metabat2 -t "${threads}" -i ../"${file}".contigs_1.5kb.fa  -m 1500 -a ./${file}_megahit_full_depth.txt -o ./"${file}"_metabat2/"${file}"_mtb &> "${file}"_megahit_metabat2.log

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
