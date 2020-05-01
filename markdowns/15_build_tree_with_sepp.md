## 5. Build tree with [SEPP QIIME 2 plugin][8]

[SEPP][9] is one method for placing short sequences into a reference phylogenetic tree. This is a useful way of determining a phylogenetic tree for your ASVs. **For 16S data** you can do this with q2-fragment-insertion using the below command:

You DO NOT need to run this command. This has already been run for you.

```bash
qiime fragment-insertion sepp \
   --i-representative-sequences deblur_output/rep_seqs_final.qza \
   --i-reference-database /home/bioinfo/tax/rRNA_db/16S/sepp-refs-gg-13-8.qza \
   --o-tree asvs-tree.qza \
   --o-placements insertion-placements.qza \
   --p-threads $NCORES
```

!!! note

    Note that if you would like to have this file locally you will need to download `sepp-refs-gg-13-8.qza` as specified in the [fragment-insertion instructions][29]. You can specify custom reference files to place other amplicons, but the easiest approach for **18S and ITS data** is to instead create a [_de novo_ tree][22].

[8]: https://github.com/qiime2/q2-fragment-insertion
[9]: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5904434/
[22]: https://github.com/LangilleLab/microbiome_helper/wiki/QIIME-2-de-novo-tree-creation
[29]: https://library.qiime2.org/plugins/q2-fragment-insertion/16/
