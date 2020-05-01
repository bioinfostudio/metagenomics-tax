## 1.6 Trim primers with cutadapt

Screen out reads that do not begin with primer sequence and remove primer sequence from reads using the [cutadapt][4] QIIME 2 plugin. The below primers correspond to the 16S V6-V8 region (Bacteria-specific primer set).

```bash
qiime cutadapt trim-paired \
   --i-demultiplexed-sequences reads_qza/reads.qza \
   --p-cores $NCORES \
   --p-front-f ACGCGHNRAACCTTACC \
   --p-front-r ACGGGCRGTGWGTRCAA \
   --p-discard-untrimmed \
   --p-no-indels \
   --o-trimmed-sequences reads_qza/reads_trimmed.qza
```

If you received the error `--p-cores option requires an argument` make sure that you set the `NCORES` bash variable.


If using 16S V4/V5 primers, use these options in the above command: 
```
   --p-front-f GTGYCAGCMGCCGCGGTAA \
   --p-front-r CCGYCAATTYMTTTRAGTTT \
```

If using 16S V6/V8 Archaeal primers, use these options in the above command: 
```
   --p-front-f TYAATYGGANTCAACRCC \
   --p-front-r CRGTGWGTRCAAGGRGCA \
```

If using 18S V4 primers, use these options in the above command: 
```
   --p-front-f CYGCGGTAATTCCAGCTC \
   --p-front-r AYGGTATCTRATCRTCTTYG \
```

If using Fungal ITS2 primers, use these options in the above command: 
```
   --p-front-f GTGAATCATCGAATCTTTGAA \
   --p-front-r TCCTCCGCTTATTGATATGC \
```


## 1.7 Summarize trimmed FASTQs

You can run the `demux summarize` command after trimming the reads to get a report of the number of reads per sample and quality distribution across the reads. This generates a more basic output compared to FASTQC/MultiQC, but is sufficient for this step.

```bash
qiime demux summarize \
   --i-data reads_qza/reads_trimmed.qza \
   --o-visualization reads_qza/reads_trimmed_summary.qzv
```

Note that we gave the output file above the extension `.qzv` since this a special type of artifact file - a **visualization**. You can look at the visualization file `reads_trimmed_summary.qzv` on the [QIIME2 view website][3]{:target="_blank"} and clicking on the `Interactive Quality Plot` tab at the top of the page

[3]: https://view.qiime2.org/?src=https://storage.googleapis.com/bioinfostudio/tax/results/reads_trimmed_summary.qzv
[4]: http://cutadapt.readthedocs.io/en/stable/guide.html
