## 2.1 Join paired-end reads

First we need to join the overlapping Illumina Pair End (PE) reads for each sample.

Currently deblur doesn't support unjoined paired-end reads. Forward and reverse reads can be joined with [VSEARCH][7] as shown below.

```bash
qiime vsearch join-pairs \
   --i-demultiplexed-seqs reads_qza/reads.qza \
   --o-joined-sequences reads_qza/reads_joined.qza
```

[7]: https://github.com/torognes/vsearch