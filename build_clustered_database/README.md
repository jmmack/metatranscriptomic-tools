Step 1) Pull genome files (see `build_database_new.sh`)

Step 2) Cluster ORFs to remove redundancy


This workflow came from:
`/Volumes/rhamnosus/reference_genomes/may2013/cluster/uclust/`

The `.ffn` reference sequences were concatenated into one file

Because of memory limitations, I couldn't use true centroid clustering. I sorted the sequences be deviation from median length and clustered from there

````
# June 21, 2013 - JM
/Volumes/rhamnosus/reference_genomes/may2013/cluster/uclust/README

# Had to remove any seqs containing non-coding RNA because we were getting abundant 16S etc. mappings. Removed by BLAST:
/Volumes/rhamnosus/reference_genomes/may2013/ncRNA_removal/README


# Do the clustering on sequences sorted by deviation from median seq length
# Try at 95% id and 90% id
nohup usearch -cluster_smallmem ../../ncRNA/all_bac_ncRNArm_medianorder.ffn -id 0.90 -centroids all_bac_ncRNArm_medianorder_id90.fasta -uc all_bac_ncRNArm_medianorder_id90.uc -usersort > nohup_id90.out 2>&1&
nohup usearch -cluster_smallmem ../../ncRNA/all_bac_ncRNArm_medianorder.ffn -id 0.95 -centroids all_bac_ncRNArm_medianorder_id95.fasta -uc all_bac_ncRNArm_medianorder_id95.uc -usersort > nohup_id95.out 2>&1&

# June 25/26 2013 - JM
- Get the taxonomy information for each cluster (lowest common taxonomy)

./get_cluster_taxonomy.pl > cluster_tax_lookup.txt
````

