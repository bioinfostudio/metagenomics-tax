## 2.3 Running deblur

Run the [deblur][5] workflow to correct reads and get amplicon sequence variants (ASVs). Note that the below command will retain singletons, which would have been filtered out unless we set ```--p-min-reads 1```, and is for 16S sequences only. For other amplicon regions, you can either use the ```denoise-other``` option in the command and specify a reference database of sequences to use for positive filtering (as in the below versions for 18S and ITS) or use DADA2 as described below (the former still being preferred due to speed considerations).

Note that you will need to trim all sequences to the same length with the ```--p-trim-length``` option if you get an error. In order to determine the correct length to trim down to, take a look at the summary visualization in order to select a length to trim back to that maintains the largest/acceptable quantity of reads. Finally, input that length in the deblur option ```--p-trim-length``` below and rerun the command.

```
qiime deblur denoise-16S \
   --i-demultiplexed-seqs reads_qza/reads_trimmed_joined_filt.qza \
   --p-trim-length 400 \
   --p-sample-stats \
   --p-jobs-to-start $NCORES \
   --p-min-reads 1 \
   --output-dir deblur_output
```

When running 18S and ITS data with deblur you will need to specify custom reference files, which can be downloaded [here][21].

!!! info

    For the **18S version** (note the first command imports the deblur database and only needs to be run once on your system):

    ```bash
    qiime tools import \
       --input-path /home/bioinfo/tax/rRNA_db/gb203_pr2_all_10_28_99p_clean_prob-rm.fasta \
       --output-path /home/bioinfo/tax/rRNA_db/gb203_pr2_all_10_28_99p_clean_prob-rm.qza \
       --type 'FeatureData[Sequence]'

    qiime deblur denoise-other \
       --i-demultiplexed-seqs reads_qza/reads_trimmed_joined_filt.qza \
       --i-reference-seqs /home/bioinfo/tax/rRNA_db/gb203_pr2_all_10_28_99p_clean_prob-rm.qza \
       --p-trim-length -1 \
       --p-sample-stats \
       --p-jobs-to-start $NCORES \
       --p-min-reads 1 \
       --output-dir deblur_output
    ```


!!! info

    For the **ITS version** (note the first command imports the deblur database and only needs to be run once on your system):
   
    ```bash
    qiime tools import \
       --input-path /home/bioinfo/tax/rRNA_db/UNITE_sh_refs_qiime_ver8_99_s_all_02.02.2019.fasta \
       --output-path /home/bioinfo/tax/rRNA_db/UNITE_sh_refs_qiime_ver8_99_s_all_02.02.2019.qza \
       --type 'FeatureData[Sequence]'
   
    qiime deblur denoise-other \
       --i-demultiplexed-seqs reads_qza/reads_trimmed_joined_filt.qza \
       --i-reference-seqs /home/bioinfo/tax/rRNA_db/UNITE_sh_refs_qiime_ver8_99_s_all_02.02.2019.qza \
       --p-trim-length -1 \
       --p-sample-stats \
       --p-jobs-to-start $NCORES \
       --p-min-reads 1 \
       --output-dir deblur_output
    ```

[5]: https://github.com/biocore/deblur
[21]: http://kronos.pharmacology.dal.ca/public_files/deblur_ref/
