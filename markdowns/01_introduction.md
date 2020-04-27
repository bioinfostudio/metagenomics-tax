## Introduction

### De novo OTU picking and diversity analysis using Illumina data

The workflow for 16S analysis in general is as follows:

1. Split multiplexed reads to samples
2. Join overlapping read pairs
4. Filter reads on quality and length
5. Filter Chimera sequences
6. Assign reads to samples
7. Pick operational taxonomic units (OTUs) for each sample
8. Alpha diversity analysis and rarefaction
9. Beta diversity analysis and Taxonomic composition
10. PCA analysis
 

16S analysis is a method of microbiome analysis (compared to shotgun metagenomics) that targets the 16S ribosomal RNA gene, as this gene is present in all prokaryotes. It features regions that are conserved among these organisms, as well as variable regions that allow distinction among organisms. These characteristics make this gene useful for analyzing microbial communities at reduced cost compared to metagenomic techniques. A similar workflow can be applied to eukaryotic micro-organisms using the 18S rRNA gene.


The tutorial dataset was originally used in a project to determine whether knocking out the protein chemerin affects gut microbial composition. Originally 116 mouse samples acquired from two different facilities were used for this project (only 24 samples were used in this tutorial dataset, for simplicity). 

## Requirements

This workflow assumes that you have QIIME 2 (version 2020.2) installed in a conda environment and that you also have [FASTQC][15] and [MultiQC][16] installed in this environment.

This workflow also assumes that the input is raw paired-end MiSeq data in demultiplexed FASTQ format located within a folder called `raw_data`. The filenames are expected to look like this: `105CHE6WT_S325_L001_R1_001.fastq.gz`, where each field separated by an `_` character corresponds to:

1. The sample name (_105CHE6WT_)
2. The sample number on the run (_S325_)
3. The lane number (_L001_)
4. The read number (_R1_ for forward and _R2_ for reverse)
5. The set number (_001_)

Often you will need to re-name your files to match this syntax. However, QIIME 2 accepts many different formats so if your files are not already in this format (e.g. not demultiplexed) you would just need to use slightly different commands for importing your data.

### 1.1 Format metadata file

You can format the metadata file (which is in a compatible format to the QIIME 1 mapping files) in a spreadsheet and validate the format using a google spreadsheet plugin as described [on the QIIME 2 website][2]. The only required column is the sample id column, which should be first. All other columns should correspond to sample metadata. Below, we assume that your metadata filename has been assigned to a bash variable called "$METADATA".

This can be done like so (for example if your file is called `metadata.txt` and is found in the folder `/home/bioinfo`):

```
METADATA="/home/bioinfo/metadata.txt"
```

The first column is the sample IDs, the next 2 are blank (note the file is tab-delimited, meaning each column is separated by a tab, not just whitespace) and the 4th column contains FASTA filenames (these filenames are based on what we will produce in this pipeline). The rest of the columns are metadata about the samples.

Here is what the first 4 lines should look like:

```
SampleID       BarcodeSequence LinkerPrimerSequence    FileInput       Source  Mouse#  Cage#   genotype        SamplingWeek
105CHE6WT                       105CHE6WT_S325_L001.assembled_filtered.nonchimera.fasta BZ      BZ25    7       WT      wk6
106CHE6WT                       106CHE6WT_S336_L001.assembled_filtered.nonchimera.fasta BZ      BZ26    7       WT      wk6
107CHE6KO                       107CHE6KO_S347_L001.assembled_filtered.nonchimera.fasta BZ      BZ27    7       chemerin_KO     wk6
```

!!! note "Note"
    The Barcode and LinkerPrimerSequence are absent for this tutorial, these would be used for assigning multiplexed reads to samples and for quality control. Our tutorial data set is already de-multiplexed. What QIIME could be used? 
 

### 1.2 Set number of cores

Several commands throughout this workflow can run on multiple cores in parallel. How many cores to use in these cases will be saved to the `NCORES` variable defined below. We set this variable to 1 below, but you can change this to be however many cores you would like to use.

```
NCORES=1
```

[2]: https://docs.qiime2.org/2020.2/tutorials/metadata/#metadata-formatting-requirements
[15]: https://www.bioinformatics.babraham.ac.uk/projects/fastqc/
[16]: https://multiqc.info/
