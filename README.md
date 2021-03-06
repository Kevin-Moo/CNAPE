# CNAPE
**C**opy **N**umber **A**lteration **P**rediction from gene **E**xpression in human cancers


## Ownership

[Wang Lab at HKUST](http://wang-lab.ust.hk/)

## Status
Active development


## Introduction

Copy number alterations (CNAs) are important features of human cancer. While the standard methods for CNA detection (CGH arrays, SNP arrrays, DNA sequencing) rely on DNA, occasionally DNA data are not available, especially in cancer studies (e.g. biopsies, legacy data). CNAPE comes into play by predicting CNAs based on gene expression data from RNA-seq.

## How to run
### 1. Installation
Before installing CNAPE please make sure you have installed [R](https://cran.r-project.org/), and ```Rscript``` is available in your system path ($PATH).

A simple clone of the repository is enough for installation, since the necessary packages will be installed automatically when you run CNAPE.
```
git clone https://github.com/WangLabHKUST/CNAPE
```
### 2. Preparing the input files
CNAPE.R takes the gene expression matrix of the human cancer samples as input. For RNA-seq data, you can process them using [TCGA's RNA-seq processing pipeline](https://webshare.bioinf.unc.edu/public/mRNAseq_TCGA/UNC_mRNAseq_summary.pdf) (i.e., reads were
aligned to the human genome using [MapSplice](https://academic.oup.com/nar/article/38/18/e178/1068935) and expression was quantified/normalized using [RSEM](https://bmcbioinformatics.biomedcentral.com/articles/10.1186/1471-2105-12-323) against UCSC genes).

An example input file demonstrating the format of the input gene expression matrix can be found in the *example/* folder.
### 3. Running CNAPE
The main function of CNAPE is packaged in *cnape.R*. Get your gene expression profile prepared, and run it like this:

```
Rscript cnape.R expressionMatrix outputPrefix
```


The output contains *prefix*.chromosome_level.cna.txt and *prefix*.arm_level.cna.txt, where 1 means amplified, -1 means deleted, while 0 means no CNA change.
### 4. Examples
#### Large-scale CNAs
For chromosome and arm level CNAs, the models trained on TCGA pan-cancer data are available. After you have cloned CNAPE, please go to the CNAPE folder and run :
```
./run_example.sh
```
Your result files, named example.chromosome_level.cna.txt and example.arm_level.cna.txt, should appear in the example folder. You can compare the results with the provided example.chromosome_level.cna.origional.txt and example.arm_level.cna.origional.txt.

#### Gene-level CNAs
A more detailed [example](example/Example_copy_number_alteration_in_glioma.md) on gene-level CNA prediction is provided, using the open-access TCGA pan-glioma data. In this example you will see how the models are formulated and trained, as well as their performance in testing. We also show how you can extract the feature genes in the models.

## Dependencies

The models are trained on the [TCGA Pancancer Atlas data](https://gdc.cancer.gov/about-data/publications/pancanatlas), using [*glmnet*](https://web.stanford.edu/~hastie/glmnet/glmnet_alpha.html) package in R. The dependency requirements are automatically solved while running the program.

## Contact
For technical issues please send an email to qmu@connect.ust.hk or jgwang@ust.hk.
