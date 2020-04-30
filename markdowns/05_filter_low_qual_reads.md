## 2.2 Filter out low-quality reads

This command will filter out low-quality reads based on the default options.

```bash
qiime quality-filter q-score-joined \
   --i-demux reads_qza/reads_joined.qza \
   --o-filter-stats filt_stats.qza \
   --o-filtered-sequences reads_qza/reads_trimmed_joined_filt.qza
```

It is a good idea at this point just to verify that there haven't been any substantial losses of reads, before going through the whole ASV process, at either the joining or quality-filtering steps:

```bash
qiime demux summarize \
   --i-data reads_qza/reads_trimmed_joined_filt.qza \
   --o-visualization reads_qza/reads_trimmed_joined_filt_summary.qzv
```
