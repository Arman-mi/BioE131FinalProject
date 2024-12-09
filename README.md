# BioE131FinalProject
step 1: setup you AWS acount. please refer to the instructions listed on Lab 8 on how to setup your AWS acount.
step 2: setup Jbrowse according to the isntructions listed on Lab 8.
step 3 : Ensure AWS enviroment is set up by running the following command : export APACHE_ROOT=/var/www/html
step 4: make sure ubuntu has the correct permissions : sudo chown -R $(whoami) $APACHE_ROOT/jbrowse2
requried tools : 
wget: For downloading genome and annotation files.
samtools: For indexing genome files.
minimap2: For sequence alignment.
JBrowse CLI: For adding assemblies and tracks.
using the wget -O command please download the provided genomes to jbrowse example : 

