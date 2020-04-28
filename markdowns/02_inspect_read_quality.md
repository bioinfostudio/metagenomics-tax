### 1.3 Inspect read quality

Visualize sequence quality across raw reads. This is important as a sanity check that your reads are of reasonable quality and to determine how your reads should be trimmed in downstream steps. QIIME 2 comes with a plugin for visualizing read quality, which we will use at a later step. However, when dealing with raw reads the easiest method to use is a combination of [FASTQC][15] and [MultiQC][16]. Note that these tools are not packaged with QIIME 2 so you will need to install them separately.

This is an important step for identifying outlier samples with especially low quality, read sizes, read depth, and other metrics.

You can run FASTQC with this command (after creating the output directory).
```
mkdir fastqc_out
fastqc -t $NCORES raw_data/*.fastq.gz -o fastqc_out
```

If you receive the error `Value "FASTQ" invalid for option threads (number expected)` (where "FASTQ" is an input filename) then make sure you have defined the `NCORES` variable correctly and re-run the command.

FASTQC generates a report for each individual file. To aggregate the summary files into a single report we can run MultiQC with these commands (including entering and leaving the FASTQC output directory):

```
cd fastqc_out
multiqc .
```

The full report is found within [multiqc_report.html](repo:results/multiqc_report.html) in the FASTQC output directory. The most important reason to visualize this report is to ensure that your samples are of high-quality (based largely on whether the per-base quality is >30 across most of the reads) and that there are no outlier samples.
 

### 1.5 Import FASTQs as QIIME 2 artifact

To standardize QIIME 2 analyses and to keep track of provenance (i.e. a list of what commands were previously run to produce a file) a special format is used for all QIIME 2 input and output files called an "artifact" (with the extension QZA). The first step is to import the raw reads as a QZA file.

```
mkdir reads_qza
    
qiime tools import \
   --type SampleData[PairedEndSequencesWithQuality] \
   --input-path raw_data/ \
   --output-path reads_qza/reads.qza \
   --input-format CasavaOneEightSingleLanePerSampleDirFmt
```

All of the FASTQs are now in the single artifact file `reads_qza/reads.qza`. This file format can be a little confusing at first, but it is actually just a zipped folder. You can manipulate and explore these files better with the `qiime tools` utilities (e.g. `peek` and `view`).

[15]: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
[16]: https://multiqc.info/
