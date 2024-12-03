# input_annotation

Cryptococcus H99 genome annotation files used for read alignment and counting.

## Cryptococcus_neoformans_var_grubii_h99.CNA3.31.dna.genome.fa

The DNA (chromosome) sequences in fasta format, from the Broad's CNA3 [CRYPTOCOCCUS NEOFORMANS SEROTYPE A GENOME PROJECT](https://www.broadinstitute.org/fungal-genome-initiative/cryptococcus-neoformans-serotype-genome-project)

## CNA3_chrlengths.txt

Just the chromosome lengths from the fasta file.

## H99.10p.aATGcorrected.2018-12-03.gff3

Annotation of genomic features including genes, exons, CDS, 
Produced by Corinne Maurice and Guilhem Janbon, the original version is in [CryptoTranscriptome2018](https://github.com/ewallace/CryptoTranscriptome2018).
This was part of the work in [Wallace, Maurice, et al, Nucleic Acids Research 2020]()

Use `H99.10p.aATGcorrected.2018-12-03.gff3` for the annotation track on the genome browser; or make subsets for mapping smaller numbers of features.

## H99.mRNAonly.2018-12-03.gff

This just includes mRNA features as a single (unspliced) feature from end to end, taken from `H99.10p.aATGcorrected.2018-12-03.gff3`.
Use `H99.mRNAonly.2018-12-03.gff` to assign reads to (unspliced) mRNA regions.
