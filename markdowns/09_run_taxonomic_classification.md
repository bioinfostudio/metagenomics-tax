### 3.2 Run taxonomic classification

You can run the taxonomic classification with this command, which is one of the longest running and most memory-intensive command of the SOP. If you receive an error related to insufficient memory (and if you cannot increase your memory usage) then you can look into the `--p-reads-per-batch` option and set this to be lower than the default (which is dynamic depending on sample depth and the number of threads) and also try running the command with fewer jobs (e.g. set `--p-n-jobs 1`).

```bash
qiime feature-classifier classify-sklearn \
   --i-reads deblur_output/representative_sequences.qza \
   --i-classifier /home/shared/taxa_classifiers/qiime2-2020.2_classifiers/classifier_silva_132_99_16S.qza \
   --p-n-jobs $NCORES \
   --output-dir taxa
```

As with all QZA files, you can export the output file to take a look at the classifications and confidence scores:

```bash
qiime tools export \
   --input-path taxa/classification.qza --output-path taxa
```
