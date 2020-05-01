## 9. Identifying differentially abundant features with ANCOM

[ANCOM][12] is one method to test for differences in the relative abundance of features between sample groupings. It is a compositional approach that makes no assumptions about feature distributions. However, it requires that all features have non-zero abundances so a pseudocount first needs to be added (1 is a typical pseudocount choice):

```bash
qiime composition add-pseudocount \
   --i-table deblur_output/deblur_table_final.qza \
   --p-pseudocount 1 \
   --o-composition-table deblur_output/deblur_table_final_pseudocount.qza
```

Then ANCOM can be run with this command; note that CATEGORY is a placeholder for the text label of your category of interest from the metadata file:

```bash
qiime composition ancom \
   --i-table deblur_output/deblur_table_final_pseudocount.qza \
   --m-metadata-file $METADATA \
   --m-metadata-column genotype \
   --output-dir ancom_output
```

[12]: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4450248/
