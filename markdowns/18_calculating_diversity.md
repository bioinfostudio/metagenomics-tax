## 8. Calculating diversity metrics and generating ordination plots

Common alpha and beta-diversity metrics can be calculated with a single command in QIIME 2. In addition, ordination plots (such as PCoA plots for weighted UniFrac distances) will be generated automatically as well. This command will also rarefy all samples to the sample sequencing depth before calculating these metrics (`--p-sampling-depth` is a placeholder for the lowest _reasonable_ sample depth; samples with depth below this cut-off will be excluded).

```bash
qiime diversity core-metrics-phylogenetic \
   --i-table deblur_output/deblur_table_final.qza \
   --i-phylogeny asvs-tree.qza \
   --p-sampling-depth 8 \
   --m-metadata-file $METADATA \
   --p-n-jobs $NCORES \
   --output-dir diversity
```

You can then produce boxplots comparing the different categories in your metadata file. For example, to create boxplots comparing the Shannon alpha-diversity metric you can use this command:

```bash
qiime diversity alpha-group-significance \
   --i-alpha-diversity diversity/shannon_vector.qza \
   --m-metadata-file $METADATA \
   --o-visualization diversity/shannon_compare_groups.qzv
```

!!! note
    Note that you can also export this or any other diversity metric file (ending in _.qza_) and analyze them with a different program.
