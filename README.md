## Diamond pipeline to map reads to SEED database

##### April 19 2017
By: Jean Macklaim

---
DIAMOND (https://github.com/bbuchfink/diamond) is a super fast sequencing aligner for protein or DNA translation (nt->protein) searches. The database was custom curated from SEED (http://www.theseed.org/wiki/Main_Page) by Jean to contain non-redundant protein sequences with assigned SEED usbsystem functions.

The SEED database: Briefly, each `fig.peg` sequence comes from an individual genome and has a subsys4 (enzymatic) functional assignment. There are many `fig.pegs` in a subsys4 category. From there, subsys4 are hierarchically organized into broader functional groups (subsys3, subssy2, subsys1) which are non-unique to a subsys4 (i.e. a subsys4 can belong to multiple subsys3).

As Jean for more information....

---
### Required to run
```
run_diamond.sh
merge_counts.pl
blast_to_counts.pl
```

On Agrajag:
DIAMOND in installed in `/Volumes/data/bin/diamond`
The SEED database (pre-formatted for DIAMOND) is `/Volumes/data/SEED_database/subsys4.dmnd`

### Running a DIAMOND search

There is a shell script `run_diamond.sh`. To run, do the following
- Make a working directory *inside* your project directory `mkdir map_seed`. Put `run_diamond.sh` in this directory.
- Inside the project directory should be a data directory (usually called `data`) containing the **demultiplexed** read files in `.fastq.gz` format/extension. The file names should look like: `F8G-2_S43_R1_001.fastq.gz` where everything before the first underscore `_` will be taken as the sample name for downstream output

Before running the script `run_diamond.sh`:
- Define the directory containing your reads (top of script)
- Two perl scripts `blast_to_counts.pl` and `merge_counts.pl` must be in the same place you are running `run_diamond.sh`

Example directory structure:
- project_name/data/reads.fastq.gz
- project_name/map_seed/run_diamond.sh

Running:
`nohup ./run_diamond.sh &`
*Note: Since this program takes a while to run, using `nohup` will push it to the background and push any output to terminal to `nohup.out`*

### Output:
A `diamond_output` directory will be created in the directory you run the script with the .daa files, the converted .m8 files, and the total counts table `all_counts.txt`

### Troubleshooting
You may need to delete the output directory and its contents to run the script again
`rm -R diamond_output`
