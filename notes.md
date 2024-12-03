# notes.md

Notes of what we did and how we ran commands for CRyptoFLC1RNAseq

# 2024-12-03

Set up up repository from https://github.com/ewallace/QuantSeqFwd_template.

Added C. neoformans input annotation from https://github.com/ewallace/CryptoGat201RNASeq repository.

## Setting up data on the Eddie server

Hunted for the data, in datastore.

Files are in directory `/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads`

We only need 
- Samples 1-30
- read 2 (forward) reads

Log in to Eddie server, [help page](https://www.wiki.ed.ac.uk/pages/viewpage.action?spaceKey=ResearchServices&title=Eddie)

```bash

ssh ewallac2@eddie.ecdf.ed.ac.uk

qlogin -q staging

# make temporary fastq directory
fastq_tmp=/exports/eddie/scratch/ewallac2/fastq_2024-12
mkdir ${fastq_tmp}
ls /exports/eddie/scratch/ewallac2/

fastq_input=/exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads
ls -l ${fastq_input}
```

Results:
```
total 62277248
-rw-r--r-- 1 ewallac2 eddie_users 749974976 Nov  1 12:07 11308_10_S10_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 726546269 Nov  1 12:07 11308_10_S10_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 769930985 Nov  1 12:07 11308_11_S11_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 751580230 Nov  1 12:07 11308_11_S11_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 810382617 Nov  1 12:07 11308_12_S12_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 784185260 Nov  1 12:07 11308_12_S12_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 692898348 Nov  1 12:07 11308_13_S13_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 649465306 Nov  1 12:07 11308_13_S13_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 621424477 Nov  1 12:07 11308_14_S14_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 593542988 Nov  1 12:07 11308_14_S14_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 562552919 Nov  1 12:07 11308_15_S15_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 531093780 Nov  1 12:07 11308_15_S15_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 621662791 Nov  1 12:07 11308_16_S16_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 589158936 Nov  1 12:07 11308_16_S16_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 668871440 Nov  1 12:07 11308_17_S17_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 657918849 Nov  1 12:07 11308_17_S17_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 745629990 Nov  1 12:07 11308_18_S18_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 704887386 Nov  1 12:07 11308_18_S18_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 612587590 Nov  1 12:07 11308_19_S19_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 590992694 Nov  1 12:07 11308_19_S19_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 717963276 Nov  1 12:07 11308_1_S1_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 731362334 Nov  1 12:07 11308_1_S1_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 712380239 Nov  1 12:07 11308_20_S20_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 682931454 Nov  1 12:07 11308_20_S20_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 389256101 Nov  1 12:07 11308_21_S21_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 362167833 Nov  1 12:07 11308_21_S21_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 601501724 Nov  1 12:07 11308_22_S22_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 563930059 Nov  1 12:07 11308_22_S22_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 676831463 Nov  1 12:07 11308_23_S23_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 643883603 Nov  1 12:07 11308_23_S23_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 676478116 Nov  1 12:07 11308_24_S24_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 665792899 Nov  1 12:07 11308_24_S24_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 674143732 Nov  1 12:07 11308_25_S25_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 652932851 Nov  1 12:07 11308_25_S25_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 612011081 Nov  1 12:07 11308_26_S26_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 586669840 Nov  1 12:07 11308_26_S26_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 550528585 Nov  1 12:07 11308_27_S27_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 534860139 Nov  1 12:07 11308_27_S27_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 607376669 Nov  1 12:07 11308_28_S28_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 584126999 Nov  1 12:07 11308_28_S28_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 421925910 Nov  1 12:07 11308_29_S29_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 404911548 Nov  1 12:07 11308_29_S29_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 775031693 Nov  1 12:07 11308_2_S2_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 750926018 Nov  1 12:07 11308_2_S2_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 506574223 Nov  1 12:07 11308_30_S30_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 480331468 Nov  1 12:07 11308_30_S30_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 738489055 Nov  1 12:07 11308_3_S3_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 710979265 Nov  1 12:07 11308_3_S3_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 726364390 Nov  1 12:07 11308_4_S4_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 694887520 Nov  1 12:07 11308_4_S4_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 651553783 Nov  1 12:07 11308_5_S5_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 642685947 Nov  1 12:07 11308_5_S5_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 439433339 Nov  1 12:07 11308_6_S6_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 406917148 Nov  1 12:07 11308_6_S6_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 721286218 Nov  1 12:07 11308_7_S7_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 710332816 Nov  1 12:07 11308_7_S7_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 641990727 Nov  1 12:07 11308_8_S8_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 625981716 Nov  1 12:07 11308_8_S8_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 605311172 Nov  1 12:07 11308_9_S9_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 579470989 Nov  1 12:07 11308_9_S9_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users    103676 Nov  1 12:07 11308_Neg_S55_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users    138970 Nov  1 12:07 11308_Neg_S55_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 588870729 Nov  1 12:07 11308_WD01_S31_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 555240437 Nov  1 12:07 11308_WD01_S31_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 499635134 Nov  1 12:07 11308_WD02_S32_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 471262411 Nov  1 12:07 11308_WD02_S32_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 808795791 Nov  1 12:07 11308_WD03_S33_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 756441276 Nov  1 12:07 11308_WD03_S33_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 971464044 Nov  1 12:07 11308_WD04_S34_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 911902480 Nov  1 12:07 11308_WD04_S34_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 561084200 Nov  1 12:07 11308_WD05_S35_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 526738842 Nov  1 12:07 11308_WD05_S35_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 609571928 Nov  1 12:07 11308_WD06_S36_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 560544064 Nov  1 12:07 11308_WD06_S36_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 531144768 Nov  1 12:07 11308_WD07_S37_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 492046199 Nov  1 12:07 11308_WD07_S37_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 462110484 Nov  1 12:07 11308_WD08_S38_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 430503009 Nov  1 12:07 11308_WD08_S38_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 524773259 Nov  1 12:07 11308_WD09_S39_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 490783991 Nov  1 12:07 11308_WD09_S39_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 778567232 Nov  1 12:07 11308_WD10_S40_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 733009292 Nov  1 12:07 11308_WD10_S40_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 487983940 Nov  1 12:07 11308_WD11_S41_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 452091963 Nov  1 12:07 11308_WD11_S41_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 673219280 Nov  1 12:07 11308_WD12_S42_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 627355447 Nov  1 12:07 11308_WD12_S42_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 711656200 Nov  1 12:07 11308_WD13_S43_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 661779440 Nov  1 12:07 11308_WD13_S43_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 408458004 Nov  1 12:07 11308_WD14_S44_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 377553998 Nov  1 12:07 11308_WD14_S44_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 323529680 Nov  1 12:07 11308_WD15_S45_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 298064289 Nov  1 12:07 11308_WD15_S45_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 314691535 Nov  1 12:07 11308_WD16_S46_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 289308809 Nov  1 12:07 11308_WD16_S46_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 307187409 Nov  1 12:07 11308_WD17_S47_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 285171542 Nov  1 12:07 11308_WD17_S47_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 617348585 Nov  1 12:07 11308_WD18_S48_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 568156331 Nov  1 12:07 11308_WD18_S48_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 217315996 Nov  1 12:07 11308_WD19_S49_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 200940739 Nov  1 12:07 11308_WD19_S49_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 969274375 Nov  1 12:07 11308_WD20_S50_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 893978591 Nov  1 12:07 11308_WD20_S50_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 645317479 Nov  1 12:07 11308_WD21_S51_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 595278613 Nov  1 12:07 11308_WD21_S51_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 530173641 Nov  1 12:07 11308_WD22_S52_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 484995795 Nov  1 12:07 11308_WD22_S52_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 482980605 Nov  1 12:07 11308_WD23_S53_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 445834312 Nov  1 12:07 11308_WD23_S53_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 378865045 Nov  1 12:07 11308_WD24_S54_R1_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 353403653 Nov  1 12:07 11308_WD24_S54_R2_001.fastq.gz
-rw------- 1 ewallac2 eddie_users      6992 Nov  6 16:57 md5checksums.txt
-rw------- 1 ewallac2 eddie_users     11942 Nov  7 10:02 sha256sums.txt
```

Next we want to use a regular expression to select only the files of interest.

```
ls -l ${fastq_input}/11308_[0-9]*_R2_001.fastq.gz
```

That worked, with 30 files:

```
-rw-r--r-- 1 ewallac2 eddie_users 726546269 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_10_S10_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 751580230 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_11_S11_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 784185260 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_12_S12_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 649465306 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_13_S13_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 593542988 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_14_S14_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 531093780 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_15_S15_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 589158936 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_16_S16_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 657918849 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_17_S17_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 704887386 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_18_S18_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 590992694 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_19_S19_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 731362334 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_1_S1_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 682931454 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_20_S20_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 362167833 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_21_S21_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 563930059 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_22_S22_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 643883603 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_23_S23_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 665792899 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_24_S24_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 652932851 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_25_S25_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 586669840 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_26_S26_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 534860139 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_27_S27_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 584126999 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_28_S28_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 404911548 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_29_S29_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 750926018 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_2_S2_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 480331468 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_30_S30_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 710979265 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_3_S3_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 694887520 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_4_S4_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 642685947 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_5_S5_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 406917148 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_6_S6_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 710332816 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_7_S7_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 625981716 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_8_S8_R2_001.fastq.gz
-rw-r--r-- 1 ewallac2 eddie_users 579470989 Nov  1 12:07 /exports/csce/datastore/biology/groups/wallace_rna/bigdata/fastq/2024-11_Exeter_Cryptococcus_Cglabrata_Scerevisiae/01_raw_reads/11308_9_S9_R2_001.fastq.gz
```

Now copy these over:

```bash
cp ${fastq_input}/11308_[0-9]*_R2_001.fastq.gz ${fastq_tmp}
ls -l ${fastq_tmp}
```

It worked! Good.

Now let's quickly make a subsampled data file. Taking the initial 10000 records (40000 lines) of sample 1.

```bash
fastq_tmp_10000reads=/exports/eddie/scratch/ewallac2/fastq_2024-12_10000reads
mkdir ${fastq_tmp_10000reads}
gzip -dkc ${fastq_tmp}/11308_1_S1_R2_001.fastq.gz | head -n 40000 | gzip > ${fastq_tmp_10000reads}/S1_R2_init10000.fastq.gz
ls -l ${fastq_tmp_10000reads}

# check fastq file
gzip -dkc ${fastq_tmp_10000reads}/S1_R2_init10000.fastq.gz | head -n 12
```

All looks good. Log out of staging node.

```bash
exit
```

## Try to run subsampled data on Eddie server

We were already logged on to Eddie, so just need to log in to a interactive session.

```bash
# create interactive session
qlogin -pe interactivemem 4 -l h_vmem=4G -l h_rt=08:00:00

# clone repository
git clone https://github.com/ewallace/CryptoFLC1RNAseq

# find the temporary files
fastq_tmp_10000reads=/exports/eddie/scratch/ewallac2/fastq_2024-12_10000reads
ls -l ${fastq_tmp_10000reads}

# look for conda environments (Edward has previously set these up)
conda env list

# There was no previous QS2022 environment, so installing it per instructions on README.md
conda create -n QS2022 nextflow=21.10.6 cutadapt=3.7 hisat2=2.2.1 samtools=1.15 fastqc=0.11.9 multiqc=1.12-0 bedtools=2.30.0 subread=2.0.1

conda activate QS2022
```

Conda took a long while to solve the environment. About ten minutes and done.



### To do next

- check nextflow runs
- set up nextflow scratch space?
- edit directory name in pipeline (/exports/eddie/scratch/ewallac2/fastq_2024-12_10000reads) DONE.
- try running pipeline on downsampled data

```bash
# go to directory & update
cd CryptoFLC1RNAseq 
git pull

# make hisat2 index
mkdir input/annotation/index/ # make directory
hisat2-build input/annotation/ANNID_RENAME.fa \
  input/annotation/index/CNA3_hisat2

# set up nextflow work dir in scratch space
nfworkdir=/exports/eddie/scratch/ewallac2/nfwork
mkdir ${nfworkdir}

# try running actual pipeline
nextflow run quantseqfwd.nf -with-dag flowchart.png -with-report -work-dir /exports/eddie/scratch/ewallac2/nfwork
```
 