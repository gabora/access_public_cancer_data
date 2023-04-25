# Collection of useful tools to access publicly available cancer datasets



## The Cancer Genome Atlas (TCGA, [website](https://www.cancer.gov/ccg/research/genome-sequencing/tcga))

TCGA is a comprehensive dataset that includes molecular profiling data from over 33 cancer types, including genomic, transcriptomic, proteomic, and clinical data. Contains both cancer and matched healthy samples. 

**Web access**: Can be access through the Genomic Data Common portal (GDC), [https://portal.gdc.cancer.gov/](https://portal.gdc.cancer.gov/)
Alternatively, hosted by Broad institute Firehose. 

### Terminal access
use the terminal to download the data from Broad

**code**:
[ref](https://www.biostars.org/p/282757/)

download `firehose_get` using the terminal:  
```sh
  wget http://gdac.broadinstitute.org/runs/code/firehose_get_latest.zip
  unzip firehose_get_latest.zip 
 ```
 if connection is refused, try to copy the link to your browser. 
 
Example 1: download clinical analysis for breast cancer:

```firehose_get -tasks clinical analyses 'latest' brca```

Example 2: download RNAseq data for all tumor types:

```firehose_get -tasks mRNAseq stddata 'latest' ```

### Download from R

```R
library(TCGAbiolinks)
library(tidyverse)

# Get the list of available projects and find those that are TCGA
TCGA_projects <- TCGAbiolinks:::getGDCprojects()$project_id %>%
    grep(pattern = "TCGA",x = ., value = TRUE)

# Check which data cetegory is available (example)
TCGAbiolinks:::getProjectSummary("TCGA-BRCA")

# $data_categories
# file_count case_count               data_category
# 1       7414       1098            Sequencing Reads
# 2       5316       1098                 Biospecimen
# 3       8889       1098       Copy Number Variation
# 4      17111       1098 Simple Nucleotide Variation
# 5       4876       1097     Transcriptome Profiling
# 6       3714       1097             DNA Methylation
# 7       2288       1098                    Clinical
# 8       4924       1095        Structural Variation
# 9        919        881          Proteome Profiling

TCGA_query <- TCGAbiolinks::GDCquery(project = TCGA_projects,
                       data.category = "Transcriptome Profiling",
                       data.type = "Gene Expression Quantification", 
                       workflow.type = "STAR - Counts")

TCGAbiolinks::GDCdownload(TCGA_query, 
                          method = "api",
                          directory = "GDCdata_25042023",
                          files.per.chunk = 50)
```
