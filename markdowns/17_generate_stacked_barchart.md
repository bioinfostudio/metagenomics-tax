## 7. Generate stacked barchart of taxa relative abundances

A more useful output is the interactive stacked bar-charts of the taxonomic abundances across samples, which can be output with this command:

```bash
qiime taxa barplot \
   --i-table deblur_output/deblur_table_final.qza \
   --i-taxonomy taxa/classification.qza \
   --m-metadata-file $METADATA \
   --o-visualization taxa/taxa_barplot.qzv
```

Now the QIIME 2 default in the above barplots is to plot each sample individually. However, in the visualizer you can label the samples according to their metadata types, but the plots are not summed together according to their metadata (as we could do in QIIME1 using the `summarize_taxa_through_plots.py` script), so we have to rerun the above command after running a new command first to group the samples by metadata - this creates a new feature table (you have to do this for each metadata category) which becomes the new input for the above same taxa barplot command (again, run each time for each metadata category). Note that CATEGORY here below is a placeholder for the text label of your category of interest from the metadata file. Also you will need to create a new metadata file (called `CATEGORY_METADATA` below) to make a barplot of this grouped data.

```
qiime feature-table group \
   --i-table deblur_output/deblur_table_final.qza \
   --p-axis sample \
   --p-mode sum \
   --m-metadata-file $METADATA \
   --m-metadata-column CATEGORY \
   --o-grouped-table deblur_output/deblur_table_final_CATEGORY.qza

qiime taxa barplot \
   --i-table deblur_output/deblur_table_final_CATEGORY.qza \
   --i-taxonomy taxa/classification.qza \
   --m-metadata-file CATEGORY_METADATA \
   --o-visualization taxa/taxa_barplot_CATEGORY.qzv
```
