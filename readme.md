# Readme

## Data
- Download from https://www.ncbi.nlm.nih.gov/variation/tools/1000genomes/
- pkd1: Chr16: 2138709 - 2185899
- pkd2: chr4_88924578-89003137

## Pre-precessing
``` terminal
# convert vcf to plink format
plink --vcf 1000G_chr4_88924578-89003137.vcf --make-bed -out pkd2
plink --vcf 1000G_chr16_2133990-2190618.vcf --make-bed -out pkd1


plink --bfile pkd2 --indep-pairwise 50 5 0.2 --maf 0.01 --hwe 1E-6 --out pkd2

plink --bfile pkd2 --extract pkd2.prune.in --recode A --out pkd2.pruned

cat pkd2.pruned.raw | cut -d " " -f7- | awk 'NR>1{print}' > pkd2.pruned.geno.txt

plink --bfile pkd1 --indep-pairwise 50 5 0.2 --maf 0.01 --hwe 1E-6 --out pkd1

plink --bfile pkd1 --extract pkd1.prune.in --recode A --out pkd1.pruned

cat pkd1.pruned.raw | cut -d " " -f7- | awk 'NR>1{print}' > pkd1.pruned.geno.txt

```
## Visualization 

See [dimentionReduction.ipynb](dimentionReduction.ipynb) or [dimentionReduction.html](dimentionReduction.html).
