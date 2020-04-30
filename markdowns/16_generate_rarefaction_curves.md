## 6. Generate rarefaction curves

A key quality control step is to plot rarefaction curves for all of your samples to determine if you performed sufficient sequencing. The below command will generate these plots (X is a placeholder for the maximum depth in your dataset, which you can determine by running the summarize command above). Depending on if you decided to exclude any samples you may not want to re-create rarefaction curves. Note however that the below command will output rarefaction curves for a range of alpha-diversity metrics (including phylogenetic metrics), whereas above the curves were based on richness (referred to as `observed_otus`) only. Also note that the `$METADATA` bash variable was defined at the first step of this SOP and simply points to the metadata table.

```
qiime diversity alpha-rarefaction \
   --i-table deblur_output/deblur_table_final.qza \
   --p-max-depth 15 \
   --i-phylogeny asvs-tree.qza \
   --m-metadata-file $METADATA \
   --o-visualization rarefaction_curves.qzv
```

For some reason, the QIIME 2 default in the above curves with the metadata file (which you can see in the visualization) is to not give you the option of seeing each sample's rarefaction curve individually (even though this is the default later on in stacked barplots!), only the "grouped" curves by each metadata type. As it can be quite important in data QC to see if you have inconsistent samples, we need to rerun the above command, but this time omitting the metadata file (use the same X for the maximum depth, as above).

```
qiime diversity alpha-rarefaction \
   --i-table deblur_output/deblur_table_final.qza \
   --p-max-depth 15 \
   --i-phylogeny asvs-tree.qza \
   --o-visualization rarefaction_curves_eachsample.qzv
```
