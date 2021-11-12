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

```


##checkM and gtdbtk
```


```
