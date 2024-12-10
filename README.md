# BioE131FinalProject
Step 1: Setup your AWS account, please refer to the instructions listed on Lab 8 on how to setup your AWS account. <br> 

Step 2: Setup Jbrowse according to the instructions listed on Lab 8. Work up until step 3.6  <br> 
please verify that JBrowse is installed using the following bash command: <br>
--version Jbrowse <br>

Step 3 : Ensure AWS enviroment is set up by running the following command : <br>
export APACHE_ROOT=/var/www/html <br>

Step 4: Run the following command to ensure you are working with the proper permissions : <br>
sudo chown -R $(whoami) $APACHE_ROOT/jbrowse2 <br>

Step 5: Run the following command to ensure tools and packages are all up to date: <br>
sudo apt upgrade



<br>General procedure: 
<br>(please note viral_genome is a place holder and you must plug in your file name for the following steps)
<br>Step 6: Use the following command to download the sequence into AWS: <br>
wget -O {Enter the name of your output file} {Enter the download link to your file}

<br>Step 7: Decompress the genome sequence file you just downloaded using the command:
<br> gunzip {Name of the compressed sequence file}

<br>Step 8: Index the genome file:
<br> samtools faidx {name of the annotation file you just decompressed}

<br>Step 9: Add annotations to your sequence:
<br> wget -O {Name of output file} {Download link to annotation file}

<br>Step 10: Decompress the annotations file you just downloaded
<br> gunzip {Name of the compressed annotations file}

<br>Step 11: 
<br> jbrowse sort-gff {Name of annotation file you just decompressed} > {Output file name.gff}

<br>Step 12:
<br> bgzip {}

<br>Step 13: 
<br> tabix {}

<br>Step 14: Add the annotations to JBrowse
<br> jbrowse add-track {Name of compressed file} --out $APACHE_ROOT/jbrowse2 --load copy

<br>Step 15: To allow seaches by gene name in JBrowse
<br> jbrowse text-index --out $APACHE_ROOT/jbrowse2

<br>Step 16: Access your JBrowse

###########################################
Make sure to always call it JBrowse2 instead of JBrowse, go up and fix where this is not the case
###########################################



<br>Copy and paste the following bash commands to recreate our database with the same genomic sequences and annotations.

2000EboVirSequence: 
```bash
wget -O 2000EboVirSequence.fna.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.fna.gz 
gunzip 2000EboVirSequence.fna.gz
samtools faidx 2000EboVirSequence.fna
jbrowse add-assembly 2000EboVirSequence.fna --out $APACHE_ROOT/jbrowse2 --load copy
```


2000EboVirSequence anotations: 
```bash

wget -O 2000EboVirSequence_annotations.gff3.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.gff.gz 
gunzip 2000EboVirSequence_annotations.gff3.gz
jbrowse sort-gff 2000EboVirSequence_annotations.gff3 > genes.gff
bgzip genes.gff
tabix genes.gff.gz
jbrowse add-track genes.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy
Add —force
jbrowse text-index --out $APACHE_ROOT/jbrowse2
```



2014EboVirSequence : 
```bash

wget -O 2014EboVirSequence.fna.gz ftp://hgdownload.soe.ucsc.edu/goldenPath/eboVir3/bigZips/KM034562v1.fa.gz
gunzip 2014EboVirSequence.fna.gz
samtools faidx 2014EboVirSequence.fna
```



annotations for  2014EboVirSequence : 
```bash

wget -O 2014EboVirSequence_annotations.bed usegalaxy.org.au/api/datasets/a6e389a98c2d16789414434a46f1f1ba/display?to_ext=bed
jbrowse sort-bed 2014EboVirSequence_annotations.bed > sorted.bed
bgzip sorted.bed
tabix sorted.bed.gz
jbrowse add-track sorted.bed.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames 2014.fna
jbrowse text-index --out $APACHE_ROOT/jbrowse2 
jbrowse text-index --assemblyNames 2014EboVirSequence_genome --out indexed.bed --file sorted2.bed
```





to add ICTV figure 4A:
```bash

wget -O ICTV4A_genome.fna https://ftp.ictv.global/sites/default/files/report_files/Filo_Fig4.v3.CG_alignment.TXT --no-check-certificate
https://www.hiv.lanl.gov/cgi-bin/FORMAT_CONVERSION/convert.cgi.gz
ftp://ictv.global/sites/default/files/report_files/Filo_Fig4.v3.CG_alignment.TXT
Format converter: Download (https://www.hiv.lanl.gov/cgi-bin/FORMAT_CONVERSION/convert.cgi)
```



to add the GenBank : ASM3409842v1 ( 2015EboVirSequence)
```bash

wget -O  2015EboVirSequence.fna.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/034/098/425/GCA_034098425.1_ASM3409842v1/GCA_034098425.1_ASM3409842v1_genomic.fna.gz
gunzip  2015EboVirSequence.fna.gz
samtools faidx  2015EboVirSequence.fna
jbrowse add-assembly   2015EboVirSequence.fna --out $APACHE_ROOT/jbrowse2 --load copy
```
adding anotations for : ASM3409842v1 ( 2015EboVirSequence)
```bash
wget -O  2015EboVirSequence_annotations.gff3.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/034/098/425/GCA_034098425.1_ASM3409842v1/GCA_034098425.1_ASM3409842v1_genomic.gff.gz 
gunzip  2015EboVirSequence_annotations.gff3.gz
jbrowse sort-gff  2015EboVirSequence_annotations.gff3 >  2015EboVirSequence_sorted.gff
bgzip  2015EboVirSequence_sorted.gff
tabix  2015EboVirSequence_sorted.gff.gz
jbrowse add-track  2015EboVirSequence_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames  2015EboVirSequence_anotated.fna
jbrowse text-index --out $APACHE_ROOT/jbrowse2
```

adding GenBank: ASM90009415v1 (2016EboVirSequence)
```bash

wget -O 2016EboVirSequence.fna.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/900/094/155/GCA_900094155.1_ASM90009415v1/GCA_900094155.1_ASM90009415v1_genomic.fna.gz 
gunzip 2016EboVirSequence.fna.gz 
samtools faidx 2016EboVirSequence.fna
jbrowse add-assembly  2016EboVirSequence.fna --out $APACHE_ROOT/jbrowse2 --load copy
```
Adding annotations for ASM90009415v1
```bash

wget -O 2016EboVirSequence_annotations.gff3.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/900/094/155/GCA_900094155.1_ASM90009415v1/GCA_900094155.1_ASM90009415v1_genomic.gff.gz
gunzip 2016EboVirSequence_annotations.gff3.gz
jbrowse sort-gff 2016EboVirSequence_annotations.gff3 > 2016EboVirSequence_sorted.gff
bgzip 2016EboVirSequence_sorted.gff
tabix 2016EboVirSequence_sorted.gff.gz
jbrowse add-track 2016EboVirSequence_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames 2016EboVirSequenceAnotated.fna
jbrowse text-index --out $APACHE_ROOT/jbrowse2
```

<br> Create a Multiple Sequence Alignment using MAFFT
























