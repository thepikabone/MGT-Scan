Modified GT-Scan
==============



This program is a slightly modified version of the **GT-Scan**. In this version, multiple sequences in a single
fa file can be searched simultaneously, depending on the number of CPU cores. The original version can be
found [Here](https://gt-scan.csiro.au/).

#1. First, download and add [bowtie](http://bowtie-bio.sourceforge.net/tutorial.shtml) to your $PATH variable in  **$HOME/.bashrc**. 
```
export PATH=$PATH:/your/bowtie/path
```

#2. On the [bowtie](http://bowtie-bio.sourceforge.net/tutorial.shtml) website, download the pre-built indexes for H. sapiens, UCSC hg19 from the right sidebar.


#3. Clone the repository from this page by using the following command. 
```
git clone https://github.com/thepikabone/MGT-Scan
```


#4. Enter **MGT-Scan** directory and and unzip the pre-built indexes from step 2 into the **genome** directory. Remember this is your genome path. 
```
cd MGT-Scan
cd genome
unzip /your/downloaded/file
````

#5. Go back into **MGT-Scan** directory and enter **gt-scan** directory.
```
cd ..
cd gt-scan
````

#6. Edit **config.ini** and specify the path (**ref_genome_dir**) to the your **genome** path from step 4.
```
ref_genome_dir=/your/genome/path
```

#7. Set permission of **gt-scan.py** in the **gt-scan** directory to **700**.
```
chmod 700 gt-scan.py
```

#8. Export **gt-scan** directory to environment variable in **$HOME/.bashrc**.
```
export $PATH=/your/gt-scan/path:$PATH
```

#9. Make a directory called **gtscan.db** in **/tmp**. This is where all the temporary files are stored.
Delete all files in this directory periodically.
```
cd /tmp
mkdir gtscan.db
```

#10. Go back into the MGT-Scan directory, in the console, type **R --args** , followed by the following arguments:

>a. **Directory**: Directory that contains the .fa file. 

>b. **FileName**: Name of the .fa file.  

>c. **n**: Numbers of pairs of target candidates per sequence.  

>d. **dis**: The minimum distance between individual target candidate in a pair.

>e. **Cores**: Number of CPU cores this program can use.
  
Separate each argument with a space, then hit enter when you’re finished.

For example:
```
Example: R --args /home/zw355/ModifiedGT-Scan test.fa 3 80 4
```

#11. Run GTScan.R and wait for results. The results should be a tab file with the same name as
the .fa file.
```
source("GTScan.R")
```

#12. Clear temporary .db files in /tmp/gtscan.db **after** the program is finished running.

## RESULT

The result, shown as a .tab file, may look like this:
```
chr1 714299 714318 - CGCCCGGCGCCGAAGACCGG chr1 714026 714045 + CCAACGGCCCACCTCTATGG

chr1 714299 714318 - CGCCCGGCGCCGAAGACCGG chr1 714026 714045 + CCAACGGCCCACCTCTATGG
```
Each line represents a pair of candidate sequences with their chromosome numbers, locations,
and directions. The distance between each two should be greater than the given minimum distance.
These target candidates are likely to have few to no mismatches. 

A reminder that a sequence in the fafile may produce a maximum of n pairs, but it’s possible to have no output.
