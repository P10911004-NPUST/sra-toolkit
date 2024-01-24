# sra-toolkit
Download data from NCBI-SRA

## 1. Install sra-toolkit

- From apt-get  
`$ sudo apt update`  
`$ sudo apt-get install sra-toolkit`  

- From source ([Installation tutorial](https://github.com/ncbi/sra-tools/wiki/02.-Installing-SRA-Toolkit#the-sra-toolkit-provides-64-bit-binary-installations-for-the-ubuntu-and-centos-linux-distributions-for-mac-os-x-and-for-windows))  
`$ wget --output-document sratoolkit.tar.gz https://ftp-trace.ncbi.nlm.nih.gov/sra/sdk/current/sratoolkit.current-ubuntu64.tar.gz`  
`$ tar -vxzf sratoolkit.tar.gz`  
`$ vi ~/.bashrc`
> export PATH=$PATH:$PWD/sratoolkit.3.0.0-mac64/bin

`$ source ~/.bashrc`  

## Configuration
`$ vdb-config -i  # -i open the config as interactive mode`  
### Set save file directory as current directory
1. Press "t" to move to the "TOOLS" tab (or press TAB to move one by one and ENTER)
2. Set "prefetch downloads to "**current directory**"
3. Press "s" followed by "o" to save; press "x" to exit
### Or save file directory as user defined directory
1. Press "c" to move to "CACHE"
2. Press "o" to choose location of user-repository; use up & down arrow and ENTER
3. Press TAB to shift to OK tab and press ENTER followed by "y" for yes
4. Press "t" to move to "TOOLS" tab
5. Shift the asterisk to "user-repository"
6. Press "s" followed by "o" to save; press "x" to exit

## Download accession list
1. Search for the Bioproject accession number (exp. PRJNA323955) in the NCBI database
2. Click on the SRA link within the top-right "**_Related information_**" panel
3. Click on the link "**_Send results to Run selector_**"
4. Click on the "**_Accession List_**" button within the **Download** column of the **Select** panel. Named the accession list as "**SRR_Acc_List.txt**"

## Download FASTQ
### Directly download FASTQ
    $ for i in `cat SRR_Acc_List.txt`; do
        fasterq-dump ${i};
      done;
### Official approach (prefetch + fasterq-dump)
    $ mkdir sra
    $ for i in `cat SRR_Acc_List.txt`; do
        prefetch --max-size u ${i};
      done;
    
    $ mkdir fastq
    $ for j in ./sra/*.sra; do
        fasterq-dump --threads 40 --progress --force -O ../fastq ${j};
      done;



