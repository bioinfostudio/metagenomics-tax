## 3. Assign taxonomy to ASVs

You can assign taxonomy to your ASVs using a Naive-Bayes approach implemented in the [scikit learn][10] Python library and the [SILVA][11] database.

### 3.1 Build or acquire taxonomic classifier

This approach requires that a classifier be trained in advance on a reference database. The QIIME 2 team recommends that classifiers be built specifically for primer sets analyzed. Note that in a previous iteration we **encountered issues with classifiers built on specific variable regions such as V6-V8**. The main issue is that the classifier would assign the vast majority of ASVs as the genus _Alteromonas_ for certain datasets, indicating a likely overfitting problem. This problem appears to be resolved in the latest taxa classifiers, but it's a good idea to run a few sanity checks on the output to make sure it worked correctly for your data (see below).

If you would like to try our custom 16S classifiers or require a non-16S classifier you can see the below list of classifiers. Below we will describe these classifiers, but if your primer set is not there you should check what classifiers are available on the [QIIME 2 website][27]. In addition, **it is especially important to manually check the taxonomic assignment of ASVs when using these custom classifiers to double-check that they performed properly on your dataset.** In addition, although theoretically the assignments can be improved by using primer-specific classifiers, we recommend the full-length 16S classifier be run as well whenever you are running a custom 16S classifier for the first time or on a new environment.

The custom classifiers available include ([see download][18] and [commands used to create these files](https://github.com/LangilleLab/microbiome_helper/wiki/Creating-QIIME-2-Taxonomic-Classifiers)):

- 16S V4/V5 region (```classifier_silva_132_99_16S_V4.V5_515F_926R.qza```)
- 16S V3/V4 region (```classifier_silva_132_99_16S_V3.V4_341F_805R.qza```)
- 16S V6/V8 region (```classifier_silva_132_99_16S_V6.V8_B969F_BA1406R.qza```)
- 16S V6/V8 region targeting archaea (```classifier_silva_132_99_16S_V6.V8_A956F_A1401R.qza```)
- 16S V3/V4 region targeting cyanobacteria (```classifier_silva_132_99_16S_V3.V4_CYA359F_CYA781R.qza```)
- 18S V4 region (```classifier_silva_132_99_18S.qza```)
- Full ITS - fungi only (```classifier_sh_refs_qiime_ver8_99_s_02.02.2019_ITS.qza```)
- Full ITS - all eukaryotes (```classifier_sh_refs_qiime_ver8_99_s_all_02.02.2019_ITS.qza```)


### 3.2 Run taxonomic classification

You can run the taxonomic classification with this command, which is one of the longest running and most memory-intensive command of the SOP. If you receive an error related to insufficient memory (and if you cannot increase your memory usage) then you can look into the `--p-reads-per-batch` option and set this to be lower than the default (which is dynamic depending on sample depth and the number of threads) and also try running the command with fewer jobs (e.g. set `--p-n-jobs 1`).

```bash
qiime feature-classifier classify-sklearn \
   --i-reads deblur_output/representative_sequences.qza \
   --i-classifier /home/bioinfo/tax/taxa_classifiers/qiime2-2020.2_classifiers/classifier_silva_132_99_16S.qza \
   --p-n-jobs $NCORES \
   --output-dir taxa
```

As with all QZA files, you can export the output file to take a look at the classifications and confidence scores:

```bash
qiime tools export \
   --input-path taxa/classification.qza --output-path taxa
```

[10]: http://scikit-learn.org/stable/
[11]: https://www.arb-silva.de/
[18]: http://kronos.pharmacology.dal.ca/public_files/taxa_classifiers/qiime2-2020.2_classifiers
[27]: https://docs.qiime2.org/2020.2/data-resources/
