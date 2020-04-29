## 4. Filtering resultant table

Filtering the denoised table is an important step of microbiome data analysis. You can see more details on this process in the [QIIME 2 filtering tutorial][14].

### 4.1 Filter out rare ASVs

Based on the summary visualization created in step 2.4 above you can choose a cut-off for how frequent a variant needs to be (and optionally how many samples need to have the variant) for it to be retained. One possible choice would be to remove all ASVs that have a frequency of less than 0.1% of the mean sample depth. This cut-off excludes ASVs that are likely due to MiSeq bleed-through between runs (reported by Illumina to be 0.1% of reads). To calculate this cut-off you would identify the mean sample depth in the visualization created in step 2.4, multiply it by 0.001, and round to the nearest integer.

Once you've determined how you would like to filter your table you can do so with this command (X is a placeholder for your choice):

```bash
qiime feature-table filter-features \
   --i-table deblur_output/table.qza \
   --p-min-frequency X \
   --p-min-samples 1 \
   --o-filtered-table deblur_output/deblur_table_filt.qza
```

[14]: https://docs.qiime2.org/2020.2/tutorials/filtering/
