## Kaiju for taxonomic assignment of metagenomic or metatranscriptomic reads

###### Jul 14 2017
by: Jean Macklaim

---

Kaiju (http://kaiju.binf.ku.dk) is a program that will take metagenomic or transcriptomic reads and predict the taxonomic distribution based on comparison to a database (typically acquired from NCBI)

It is supposedly faster/better than kraken (we've used this previously)

### Required to run
`run_kaiju.sh`

### Installing kaiju and database
Kaiju is installed on Agrajag:
`/data/bin/kaiju/bin`

I've already downloaded a database for running. **_You do not need to reinstall kaiju or the database unless you want a new one. Skip to Running kaiju._**

Make a database directory
`mkdir /Volumes/data/bin/kaiju/kaijudb`

Choose a database. This will change the amount of storage needed and the amount of RAM to run

```
cd kaijudb/
nohup ../bin/makeDB.sh -e &
```
"Download the nr database as above, but additionally include proteins from fungi and microbial eukaryotes."

### Running kaiju
There is a shell script `run_kaiju.sh`. To run, do the following
- You should have aworking directroy with a data directory (usually called `data`) containing the **demultiplexed** read files in `.fastq.gz` format/extension. The file names should look like: `F8G-2_S43_R1_001.fastq.gz` where everything before the first underscore `.` will be taken as the sample name for downstream output
- Paths to kaiju and kaijudb are set at the top of the script **you probably don't have to change these**, but you should set the path to your data (reads) directory


To run (assuming you have the script in your working directory):
`./run_kaiju.sh`

### Output
The `.summary` files will give the %mapped to each taxon. If you want to quickly see the top mapped for all samples try:

`head *.summary > all_summary.txt`
