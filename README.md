# Using the runTerraWorkflow on the AsnicarF_2017 study

This example will be done on a Linux operating system using the
terminal.

OS: Pop!_OS 22.04 LTS x86_64

## Download FASTQ files from the NCBI-SRA

We'll download the FASTQ files from the NCBI-SRA using the SRAToolkit. First,
we need to get the SRA identifiers. We'll get the identifiers for the 
AsnicarF_2017 study through the 
[curatedMetagenomicData command line interface](https://github.com/waldronlab/curatedMetagenomicDataTerminal).

If you have administrator permission, the curatedMetagenomicData command line 
can be installed with:

```bash
curl -sSL https://tinyurl.com/cMDTerminal | bash
```

Otherwise, you can install it with the following commands: 

```bash

## Create the bin directory at $HOME
cd $HOME
mkdir bin

Rscript -e 'utils::install.packages("BiocManager", repos = "https://cloud.r-project.org/")'
Rscript -e 'BiocManager::install("waldronlab/curatedMetagenomicDataTerminal")'
Rscript -e 'curatedMetagenomicDataTerminal::install("~/bin/curatedMetagenomicData")'

## Check that it has been installed
which curatedMetagenomicData
#> /home/samuel/bin/curatedMetagenomicData
```

Note: The latest version of R must be installed and available in the PATH.

Get AsnicarF_2017 metadata and get NCBI IDs in a text file:

```bash
curatedMetagenomicData "AsnicarF_2017.+relative_abundance" --metadata > AsnicarF_2017_metadata.tsv
awk 'BEGIN {FS="\t";OFS="\t"} NR==1{for(i=1;i<=NF;i++) f[$i] = i} { print $(f["NCBI_accession"]) }' AsnicarF_2017_metadata.tsv > sra_ids.txt
sed -i -e '/NCBI_accession/d' sra_ids.txt
head sra_ids.txt

#> SRR4052021
#> SRR4052022
#> SRR4052033
#> SRR4052038
#> SRR4052039
#> SRR4052040
#> SRR4052041
#> SRR4052042
#> SRR4052043
#> SRR4052044
```



