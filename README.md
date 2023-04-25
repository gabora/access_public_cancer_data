# Collection of useful tools to access publicly available cancer datasets



## The Cancer Genome Atlas (TCGA, [website](https://www.cancer.gov/ccg/research/genome-sequencing/tcga))

**description**: TCGA is a comprehensive dataset that includes molecular profiling data from over 33 cancer types, including genomic, transcriptomic, proteomic, and clinical data. Contains both cancer and matched healthy samples. 

**access**: Can be access through the Genomic Data Common portal (GDC), [https://portal.gdc.cancer.gov/](https://portal.gdc.cancer.gov/)
Alternatively, hosted by Broad institute Firehose

**code**:
[ref](https://www.biostars.org/p/282757/)

download `firehose_get` using the terminal:  
```{sh}
  wget http://gdac.broadinstitute.org/runs/code/firehose_get_latest.zip
  unzip firehose_get_latest.zip 
 ```
 if connection is refused, try to copy the link to your browser. 
 
Example 1: download clinical analysis for breast cancer:

```firehose_get -tasks clinical analyses 'latest' brca```

Example 2: download RNAseq data for all tumor types:

```firehose_get -tasks mRNAseq stddata 'latest' ```

