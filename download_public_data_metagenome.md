##

#use sra kit to download oil related data from db

#https://github.com/ncbi/sra-tools/wiki/08.-prefetch-and-fasterq-dump

#reference https://www.biostars.org/p/111040/
```
#

cd /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus

mkdir oil_related_metaG

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/oil_related_metaG

#
screen -r sra.download

for file in $(cat oil_related_metaG_reads.txt)
do
prefetch "${file}" &> "${file}".sra.download.txt
done

sudo /home/PTPE2/Software/sratoolkit.2.9.2-ubuntu64/bin/prefetch SRR5352268 -v --max-size 100G -O /home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/oil_related_metaG/SRR5352268

#error
2021-10-28T14:12:46 prefetch.2.9.2 int: transfer incomplete while reading file within network system module - Cannot KStreamRead: https://sra-downloadb.be-md.ncbi.nlm.nih.gov/sos2/sra-pub-run-7/SRR5352268/SRR5352268.1
2021-10-28T14:12:46 prefetch.2.9.2: 1) failed to download SRR5352268
```
