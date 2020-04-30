### 4.2 Filter out contaminant and unclassified ASVs

Now that we have assigned taxonomy to our ASVs we can use that information to remove ASVs which are likely contaminants or noise based on the taxonomic labels. Two common contaminants in 16S sequencing data are mitochondrial and chloroplast 16S sequences, which can be removed by excluding any ASV which contains those terms in its taxonomic label. It can also be useful to exclude any ASV that is unclassified at the phylum level since these sequences are more likely to be noise (e.g. possible chimeric sequences). Note that if your data has not been classified against SILVA you will need to change `D_1__` to be a string that enables phylum-level assignments to be identified or simply omit that line. You may also want to omit that line if you are studying a poorly characterized environment where you have a good chance of identifying novel phyla.

```bash
qiime taxa filter-table \
   --i-table deblur_output/deblur_table_filt.qza \
   --i-taxonomy taxa/classification.qza \
   --p-include D_1__ \
   --p-exclude mitochondria,chloroplast \
   --o-filtered-table deblur_output/deblur_table_filt_contam.qza
```
