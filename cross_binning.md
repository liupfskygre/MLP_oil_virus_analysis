##


##
```
#
ssh PTPE2@172.21.83.54
LZU_ptpe2

```


##work dir
```
/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus

#trimmed_reads
mkdir trimmed_reads

/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/trimmed_reads

#started running 20211103
/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scripts/Cross_mapping_single_5samples.sh mapping_template.txt 60


```

#sort for metabat2
```
for file in *_bbmap_binning

do
cd "${file}"

for bamfile in *.bam
do

samtools sort -@ 60 ${bamfile} > "${bamfile}".sorted

done

cd ..

done


```
