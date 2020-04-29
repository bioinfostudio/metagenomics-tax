### 3.3 Assess subset of taxonomic assignments with BLAST

The performance of the taxonomic classification is difficult to assess without a gold-standard reference, but nonetheless one basic sanity check is to compare the taxonomic assignments with the top BLASTn hits for certain ASVs.

It is simple to do this with QIIME 2 by running:

```bash
qiime feature-table tabulate-seqs --i-data deblur_output/representative_sequences.qza \
                                  --o-visualization deblur_output/representative_sequences.qzv
```

The file [representative_sequences.qzv](repo:results/representative_sequences.qzv){:target="_blank"} is a QIIME 2 visualization file that you can open in the [QIIME 2 viewer][3]. The format makes it easy to BLAST certain ASVs against the NCBI nt database. By comparing these BLAST hits with the taxonomic assignment of ASVs generated above you can reassure yourself that the taxonomic assignments overall worked correctly. It's a good idea to select ~5 ASVs to BLAST for this validation, which should be from taxonomically different groups, such as different phyla, according to the taxonomic classifier.

[3]: https://view.qiime2.org/
