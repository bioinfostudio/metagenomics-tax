### 4.4 Subset and summarize filtered table

Once we have our final filtered table we will need to subset the QZA of ASV sequences to the same set. You can exclude the low frequency ASVs from the sequence file with this command:

```
qiime feature-table filter-seqs \
   --i-data deblur_output/representative_sequences.qza \
   --i-table deblur_output/deblur_table_final.qza \
   --o-filtered-data deblur_output/rep_seqs_final.qza
```

Finally, you can make a new summary of the final filtered abundance table:

```
qiime feature-table summarize \
   --i-table deblur_output/deblur_table_final.qza \
   --o-visualization deblur_output/deblur_table_final_summary.qzv
```
