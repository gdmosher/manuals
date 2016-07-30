---
title: Load workflow environment
keywords: 
last_updated: Sat Jul 30 12:35:03 2016
sidebar: mydoc_sidebar
permalink: /mydoc/systemPipeChIPseq_02/
---

Now open the R markdown script `systemPipeChIPseq.Rmd`in your R IDE (_e.g._ vim-r or RStudio) and 
run the workflow as outlined below. 

## Load packages and sample data

The `systemPipeR` package needs to be loaded to perform the analysis steps shown in
this report (Girke , 2015).


```r
library(systemPipeR)
```

Load workflow environment with sample data into your current working
directory. The sample data are described
[here](http://www.bioconductor.org/packages/devel/bioc/vignettes/systemPipeR/inst/doc/systemPipeR.html#load-sample-data-and-workflow-templates).


```r
library(systemPipeRdata)
genWorkenvir(workflow="chipseq")
setwd("chipseq")
download.file("https://raw.githubusercontent.com/tgirke/GEN242/master/vignettes/12_ChIPseqWorkflow/systemPipeChIPseq.Rmd", "systemPipeChIPseq.Rmd")
```

In the workflow environments generated by `genWorkenvir` all data inputs are stored in
a `data/` directory and all analysis results will be written to a separate
`results/` directory, while the `systemPipeChIPseq.Rmd` script and the `targets` file are expected to be located in
the parent directory. The R session is expected to run from this parent
directory. Additional parameter files are stored under `param/`.

To work with real data, users want to organize their own data similarly
and substitute all test data for their own data. To rerun an established
workflow on new data, the initial `targets` file along with the corresponding
FASTQ files are usually the only inputs the user needs to provide.

If applicable users can load custom functions not provided by `systemPipeR`. Skip
this step if this is not the case.


```r
source("systemPipeChIPseq_Fct.R")
```

## Experiment definition provided by `targets` file

The `targets` file defines all FASTQ files and sample comparisons of the analysis workflow.


```r
targetspath <- system.file("extdata", "targets_chip.txt", package="systemPipeR")
targets <- read.delim(targetspath, comment.char = "#")
targets[1:4,-c(5,6)]
```

```
##                   FileName SampleName Factor SampleLong SampleReference
## 1 ./data/SRR446027_1.fastq        M1A     M1  Mock.1h.A                
## 2 ./data/SRR446028_1.fastq        M1B     M1  Mock.1h.B                
## 3 ./data/SRR446029_1.fastq        A1A     A1   Avr.1h.A             M1A
## 4 ./data/SRR446030_1.fastq        A1B     A1   Avr.1h.B             M1B
```

<div class="tags">
<b>Jump to: </b>
<a href="../../mydoc/systemPipeChIPseq_03/" class="btn btn-default navbar-btn cursorNorm" role="button">next_page</a>
</div>