# BioE131FinalProject
step 1: setup you AWS acount. please refer to the instructions listed on Lab 8 on how to setup your AWS acount.
step 2: setup Jbrowse according to the isntructions listed on Lab 8. --version Jbrowse 
run jbrowse --help to check the following packages and commands are installed
wget: For downloading genome and annotation files.
samtools: For indexing genome files.
minimap2: For sequence alignment. // ... check qith versions ...
JBrowse CLI: For adding assemblies and tracks.
minimap2


step 3 : Ensure AWS enviroment is set up by running the following command : export APACHE_ROOT=/var/www/html
step 4: make sure ubuntu has the correct permissions : sudo chown -R $(whoami) $APACHE_ROOT/jbrowse2
requried tools : 
*********adddd install************
run jbrowse --help to check the following packages and commands are installed
wget: For downloading genome and annotation files.
samtools: For indexing genome files.
minimap2: For sequence alignment. // ... check qith versions ...
JBrowse CLI: For adding assemblies and tracks.
(please note viral_genome is a place holder and you must plug in your file name for the following steps)
step 5: using the wget -O command please download the provided genomes to jbrowse example
step 6 : decompress the .gz file using "gunzip viral_genome.fna.gz" 
step 7 : index the genome file using samtools with the following bash command: samtools faidx viral_genome.fna
step 8 : add the file to the Jbrowse : jbrowse add-assembly viral_genome.fna --out $APACHE_ROOT/jbrowse2 --load copy
to add anotations for BED files use the following commands: 
wget -O annotations.bed.gz <put link here>
decompress and prepare the BED file : 
gunzip filoviridae_annotations.bed.gz
jbrowse sort-bed filoviridae_annotations.bed > sorted.bed
bgzip sorted.bed
tabix sorted.bed.gz
add the BED anotaion to JBrowse: jbrowse add-track sorted.bed.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames KM034562v1


to align two genome sequences using minimap2 follow the following instructions : 



minimap2 -x asm5 -c reference_genome.fasta query_genome.fasta > output.paf



use the following if a SAM format is required : minimap2 -a reference_genome.fasta query_genome.fasta > output.sam


after setting up follow the following commands to make sure everything is running smoothly 

wget -O viral_genome_annotations.gff3.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.gff.gz 
gunzip viral_genome_annotations.gff3.gz
jbrowse sort-gff viral_genome_annotations.gff3 > genes.gff
bgzip genes.gff
tabix genes.gff.gz
jbrowse add-track genes.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy
Add —force
jbrowse text-index --out $APACHE_ROOT/jbrowse2




to add an additional assembly : 
wget -O filoviridae_genome.fna.gz ftp://hgdownload.soe.ucsc.edu/goldenPath/eboVir3/bigZips/KM034562v1.fa.gz
gunzip filoviridae_genome.fna.gz
samtools faidx filoviridae_genome.fna


annotations for bed files : 
wget -O filoviridae_annotations.bed usegalaxy.org.au/api/datasets/a6e389a98c2d16789414434a46f1f1ba/display?to_ext=bed
jbrowse sort-bed filoviridae_annotations.bed > sorted.bed
bgzip sorted.bed
tabix sorted.bed.gz
jbrowse add-track sorted.bed.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames 2014.fna
jbrowse text-index --out $APACHE_ROOT/jbrowse2 
jbrowse text-index --assemblyNames filoviridae_genome --out indexed.bed --file sorted2.bed


to add ICTV figure 4A:
wget -O ICTV4A_genome.fna https://ftp.ictv.global/sites/default/files/report_files/Filo_Fig4.v3.CG_alignment.TXT --no-check-certificate
https://www.hiv.lanl.gov/cgi-bin/FORMAT_CONVERSION/convert.cgi.gz
ftp://ictv.global/sites/default/files/report_files/Filo_Fig4.v3.CG_alignment.TXT
Format converter: Download (https://www.hiv.lanl.gov/cgi-bin/FORMAT_CONVERSION/convert.cgi)

to add the GenBank : ASM3409842v1
wget -O genbank_g2.fna.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/034/098/425/GCA_034098425.1_ASM3409842v1/GCA_034098425.1_ASM3409842v1_genomic.fna.gz
gunzip genbank_g2.fna.gz
samtools faidx genbank_g2.fna
jbrowse add-assembly  genbank_g2.fna --out $APACHE_ROOT/jbrowse2 --load copy

adding anotations for : ASM3409842v1
wget -O g2_annotations.gff3.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/034/098/425/GCA_034098425.1_ASM3409842v1/GCA_034098425.1_ASM3409842v1_genomic.gff.gz 
gunzip g2_annotations.gff3.gz
jbrowse sort-gff g2_annotations.gff3 > g2_sorted.gff
bgzip g2_sorted.gff
tabix g2_sorted.gff.gz
jbrowse add-track g2_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames 2015.fna
jbrowse text-index --out $APACHE_ROOT/jbrowse2

adding GenBank: ASM90009415v1
wget -O gca3.fna.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/900/094/155/GCA_900094155.1_ASM90009415v1/GCA_900094155.1_ASM90009415v1_genomic.fna.gz 
gunzip gca3.fna.gz 
samtools faidx gca3.fna
jbrowse add-assembly  gca3.fna --out $APACHE_ROOT/jbrowse2 --load copy

Adding annotations for ASM90009415v1
wget -O gca3_annotations.gff3.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCA/900/094/155/GCA_900094155.1_ASM90009415v1/GCA_900094155.1_ASM90009415v1_genomic.gff.gz
gunzip gca3_annotations.gff3.gz
jbrowse sort-gff gca3_annotations.gff3 > gca3_sorted.gff
bgzip gca3_sorted.gff
tabix gca3_sorted.gff.gz
jbrowse add-track gca3_sorted.gff.gz --out $APACHE_ROOT/jbrowse2 --load copy --assemblyNames 2016.fna
jbrowse text-index --out $APACHE_ROOT/jbrowse2


for Genbank
wget -O viral_genome.fna.gz https://ftp.ncbi.nlm.nih.gov/genomes/all/GCF/000/848/505/GCF_000848505.1_ViralProj14703/GCF_000848505.1_ViralProj14703_genomic.fna.gz 






















