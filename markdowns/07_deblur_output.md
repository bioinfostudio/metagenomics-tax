## 2.4 Summarizing deblur output

Once a denoising pipeline has been run you can summarize the output table with the below command, which will create a visualization artifact for you to view.

```bash
qiime feature-table summarize \
   --i-table deblur_output/table.qza \
   --o-visualization deblur_output/deblur_table_summary.qzv
```

We will use this visualization later to determine the the cut-offs for filtering the table, but for now you should mainly take a look at the visualization file `deblur_table_summary.qzv` in the [QIIME 2 viewer][3]{:target="_blank"} to **ensure that sufficient reads have been retained after running deblur**. This denoising tool filters out reads that either do match to known noise or that do not match with low similarity to the expected amplicon region. If your samples have very low depth after running deblur (compared to the input read depth) this could be a red flag that either you ran the tool incorrectly, you have a lot of noise in your data, or that deblur is inappropriate for your dataset.

[3]: https://view.qiime2.org/?src=https://storage.googleapis.com/bioinfostudio/tax/results/deblur_table_summary.qzv
