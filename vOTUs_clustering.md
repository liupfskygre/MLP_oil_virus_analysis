##

#
##
#标准，criteria/cutoff
#(95% ANI - Average Nucleotide Identity and 85% AF – Aligned Fraction)
#https://github.com/weizhongli/cdhit/wiki
```
/home/PTPE2/User/liupf/Projects_liupf/mlp_oil_virus/scaffolds10k/virus_calling_out/MLP_oil_checkv_out/MLP_total_virus_final1.fasta
#4833

#https://github.com/weizhongli/cdhit/wiki/3.-User's-Guide#CDHITEST
screen -S cd-hit-cluster

/home/PTPE2/Software/cd-hit-v4.8.1-2019-0228/cd-hit-est -i MLP_total_virus_final1.fasta -o MLP_total_virus_cdhit -c 0.95 -aS 0.85 -d 400 -T 30 -M 500000 -n 10

#-n 10 for threshold 0.95-1

================================================================
Program: CD-HIT, V4.8.1 (+OpenMP), Nov 11 2021, 21:56:46
Command:
         /home/PTPE2/Software/cd-hit-v4.8.1-2019-0228/cd-hit-est
         -i MLP_total_virus_final1.fasta -o
         MLP_total_virus_cdhit -c 0.95 -aS 0.85 -d 400 -T 30 -M
         500000 -n 10

Started: Thu Nov 11 21:58:02 2021
================================================================
                            Output
----------------------------------------------------------------
total seq: 4833
longest and shortest : 2126623 and 1689
Total letters: 155424649
Sequences have been sorted

Approximated minimal memory consumption:
Sequence        : 156M
Buffer          : 30 X 614M = 18437M
Table           : 2 X 16M = 33M
Miscellaneous   : 4M
Total           : 18631M

Table limit with the given memory limit:
Max number of representatives: 4000000
Max number of word counting entries: 60171050969

# comparing sequences from          0  to        151


```


```
Program: CD-HIT, V4.8.1 (+OpenMP), Apr 07 2021, 10:57:21
Command: cd-hit-est -i MLP_total_virus_final1.fasta -o
         MLP_total_virus_cdhit -c 0.95 -aS 0.85 -d 400 -T 30 -M
         500000 -n 10

Segmentation fault (core dumped)

 ```
