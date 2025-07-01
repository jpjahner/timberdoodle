# Notes for timberdoodle analyses


GRABBING AN INTERACTIVE JOB:
```{bash}
salloc --account=evolgen --time=3:00:00
```


## alignment (using new genome)

### grabbing reference from NCBI
```{bash}
rsync --copy-links --recursive --times --verbose rsync://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/964/304/615/GCA_964304615.2_bScoRus3.2/*.fna.gz .

gunzip GCA_964304615.2_bScoRus3.2_genomic.fna.gz

grep -c "^>" GCA_964304615.2_bScoRus3.2_genomic.fna 
    ## 123
```


### remove 60 line endings
```{bash}
perl /home/jjahner/perl_scripts/remove60_fasta.pl GCA_964304615.2_bScoRus3.2_genomic.fna 
```

### change reference names to something shorter

```{bash}
perl /home/jjahner/perl_scripts/rename_scaff.pl no60_GCA_964304615.2_bScoRus3.2_genomic.fna 

mv renamed_no60_GCA_964304615.2_bScoRus3.2_genomic.fna.txt timberdoodle_genome.fna
```


### make index for bwa

```{bash}
sbatch slurm_timberdoodle_bwa_index.sh
```










### align 

```{bash}
sbatch slurm_bh2tree_runbwa.sh
```

