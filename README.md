# QuantSeqFwd_template

Template repository for QuantSeq Fwd analysis, for RNA-seq data.

This contains a pipeline to process from reads to counts-per-mRNA, and a directory structure for some quality control using R/Rmarkdown.

EDIT THIS README FILE to describe the dataset that you are analysing


# Contents

- quantseqfwd.nf - nextflow script for read processing and counting
- Rmd - directory for R markdown scripts and further data analysis after read processing
- input - directory for input
  - input/annotation - genome or transcriptome annotation used for read alignment and counting
  - input/experiment - other input files including sample sheet
- results - directory for output data and results
    - results/counts - count data and analyses of those
    - results/xxx - create specific subdirectories for other kinds of results


# How to run the read processing pipeline

This is a read processing pipeline that does read QC, trimming, alignment, and counting per transcript.
It is written in nextflow (DSL 1.0), see https://www.nextflow.io/.

## Install software dependencies

We tested package installation using miniconda and bioconda, see:
- [miniconda installation instructions[(https://docs.conda.io/en/latest/miniconda.html)
- [bioconda installation instructions](https://bioconda.github.io/user/install.html).

Once you have bioconda installed, create a conda environment called `QS2022` by running the command:

```
conda create -n QS2022 nextflow=21.10.6 cutadapt=3.7 hisat2=2.2.1 samtools=1.15 fastqc=0.11.9 multiqc=1.12-0 bedtools=2.30.0 subread=2.0.1
```

These package versions run the pipeline as of June 2022. Others might break it or require troubleshooting/upgrading.

_Note, we hope in the future to move to singularity containers for even cleaner package management._

## Before starting, prepare your annotation

Before starting, you have to choose and pick an annotation relevant to the species in question.  Make sure it includes 3' ends of mRNAs because QuantSeq is 3'-targeted. This annotation requires:

- a fasta file of your genome (or transcriptome)
- a hisat2 index built from your fasta file
- a gff describing positions and strands of the mRNAs within the fasta file

If you don't already have an index, you can build it using commands like:

```{bash }
conda activate QS2022 # activate conda environment
mkdir input/annotation/index/ # make directory
hisat2-build input/annotation/ANNID_RENAME.fa \
  input/annotation/index/ANNID_RENAME_hisat2
```

Remember to edit the fasta file name and index name as needed.


## Set the parameters in the nextflow file

Then edit the parameters in `quantseqfwd.nf` appropriate to your analysis:

- `params.input_fq_dir = 'EXPERIMENT_RENAME_fastq'` points to an input directory containing all of your fastq files 
- `params.output_dir = 'results/counts'` points to the output directory where you would like all the outputs stored.
- `params.index_dir = 'input/annotation/index'` points to the directory with input annotation in it
- `params.index_prefix = 'ANNID_RENAME_hisat2'` name of hisat2 index
- `params.mRNAgff = 'input/annotation/ANNID_RENAME_mRNAonly.gff'` name of gff file describing mRNA locations
- `params.featuretype = 'mRNA'` in the mRNA gff file Type column, the feature corresponding to mRNA that you want to count
- `params.featurename = 'Name'` in the mRNA gff file attributes column, the field that contains the name of the feature to use in the counts file
- `params.num_processes = 4` number of processes to use for parallelising adapter trimming and alignment. Increasing this can speed up running the pipeline on larger computers
- `params.adapters = 'AAAAAAAAAAAA'` is the sequencing adapter to remove, keep this as poly(A) for QuantSeq Fwd
- `params.hisat2_other = '-k 2 --pen-cansplice 4 --pen-noncansplice 12 --min-intronlen 40  --max-intronlen 200' other hisat2 parameters, these are specialised for aligning intron-poor yeast genomes, see hisat2 manual for details


## Run the pipeline on subsampled data

Remember that it is best to test & run carefully with subsampled data first, to find problems quickly!
Point 

- `params.input_fq_dir = 'EXPERIMENT_RENAME_fastq_subsample'` points to an input directory containing all of your fastq files 
- `params.output_dir = 'results/counts_subsample'` points to the output directory where you would like all the outputs stored.

Then run the command:

```{bash }
conda activate QS2022 
nextflow run quantseqfwd.nf -with-dag flowchart.png -with-report counts_subsample/nextflow_report.html
```

The options `-with-dag` and `-with-report` are just to tell you a little more about the output, they are not strictly needed in order to run.
The flowchart shows what steps happen in the pipeline.

Troubleshoot (installation, filepaths, etc) until everything works.

At this point it's helpful to `git commit` the subsampled run data in `results/counts_subsample`, along with notes of anything you changed.


## Run the pipeline on full-size data

Edit
-  `params.input_fq_dir`  to point to the full input dataset
-  `params.output_dir = 'results/counts'` or elsewhere as desired

Then run:

```{bash }
conda activate QS2022 
nextflow run quantseqfwd.nf -with-report counts/nextflow_report.html
```

Save the results, i.e. the contents of `results/counts`.


## Inspect the results

TBA


## Check the reproducibility of results using the R markdown file

### Install R & RStudio

https://www.rstudio.com/products/rstudio/download/

Then install packages. Either use RStudio GUI or run:

```r
install.packages("tidyverse","cowplot","GGally","here")
if (!require("BiocManager", quietly = TRUE))
    install.packages("BiocManager")

BiocManager::install("biobroom","DESeq2")
```

More info at Jeffrey Leek's Data Scientist Toolbox:
https://jtleek.com/modules/01_DataScientistToolbox/02_09_installingRPackages/#5

### Rename the R project file

Give the file `QSFwd_RENAME.Rproj` a name that describes your actual project.
You can then return to the project by opening that file.

Then open this R project file in RStudio

### Quality control of read counts wiht scatter plots and PCA

From RStudio, open the file `Rmd/QC_PCA.Rmd`.
Edit the parts needed to describe your dataset (marked by `EDIT` or `RENAME`).

Load the count data using the code present then begin to troubleshoot data loading and visualisation.

The goal is to have everything running smoothly up to the point where you can press "knit", and a complete documented analysis all runs in one go, with informative figures, output, and thoughts.

