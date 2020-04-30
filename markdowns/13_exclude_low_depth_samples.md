### 4.3 Exclude low-depth samples

Often certain samples will have quite low depth after these filtering steps, which can be excluded from downstream analyses since they will largely add noise. There is no single cut-off that works best for all datasets, but researchers often use minimum cut-offs within the range of 1000 to 4000 reads. You can also use a cut-off much lower than this if you want to retain all samples except those that failed entirely (e.g. depth < 50 reads). Ideally you would choose this cut-off after visualizing rarefaction curves to determine at what read depth the richness of your samples plateaus and choose a cut-off as close to this plateau as possible while retaining sufficient sample size for your analyses.

To perform this rarefaction curve analysis you would first need to summarize the filtered table we produced in the last step:
```
qiime feature-table summarize \
   --i-table deblur_output/deblur_table_filt_contam.qza \
   --o-visualization deblur_output/deblur_table_filt_contam_summary.qzv
```

From this table you need to determine the maximum depth across your samples. You can then generate the rarefaction curves with this command (where `X` is a placeholder for the max depth across samples).

```
qiime diversity alpha-rarefaction \
   --i-table deblur_output/deblur_table_filt_contam.qza \
   --p-max-depth 15 \
   --p-metrics 'observed_otus' \
   --o-visualization rarefaction_curves_test.qzv
```

Take a look at these curves to help decide on a minimum depth cut-off for retaining samples. Once you decide on a hard cut-off you can exclude samples below this cut-off with this command (where `SET_CUTOFF` is a placeholder for the minimum depth you select):

```
qiime feature-table filter-samples \
   --i-table deblur_output/deblur_table_filt_contam.qza \
   --p-min-frequency 6 \
   --o-filtered-table deblur_output/deblur_table_final.qza
```

**Alternatively, if you do not wish to exclude any samples** then you can simply make a copy of the QZA file with the final table filename (i.e. `cp deblur_output/deblur_table_filt_contam.qza deblur_output/deblur_table_final.qza`), since this is the filename used for the remaining commands below.
