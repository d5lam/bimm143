Class 15 Pathway Analysis and Gene List Interpretation
================
Darren Lam
11/14/2019

# Pathway analysis

An enriched pathway results from the overlap between differentially
expressed genes (DEGs) and known pathways (genesets)

Limitations to pathway analysis include: geneset annotation bias,
non-model organisms, ignoring post-transcriptional regulation,
tissue-specific vatiations not annotated, size bias

### Overview

1)  You have a list of genes/proteins of interest (and info on fold
    change, p-value, spectral counts, presence/absence)
2)  Translate to appropriate identifier (e.g. UniProt, Entrez, etc)
    using merge() or mapIds()

# Hands-on worksheet

Reading in our colData and countData

``` r
colData = read.csv("GSE37704_metadata.csv", row.names = 1)
head(colData)
```

    ##               condition
    ## SRR493366 control_sirna
    ## SRR493367 control_sirna
    ## SRR493368 control_sirna
    ## SRR493369      hoxa1_kd
    ## SRR493370      hoxa1_kd
    ## SRR493371      hoxa1_kd

``` r
countData = read.csv("GSE37704_featurecounts.csv", row.names = 1)
countData <- as.matrix(countData[,-1]) # removed first column so countData columns match colData rows
head(countData)
```

    ##                 SRR493366 SRR493367 SRR493368 SRR493369 SRR493370
    ## ENSG00000186092         0         0         0         0         0
    ## ENSG00000279928         0         0         0         0         0
    ## ENSG00000279457        23        28        29        29        28
    ## ENSG00000278566         0         0         0         0         0
    ## ENSG00000273547         0         0         0         0         0
    ## ENSG00000187634       124       123       205       207       212
    ##                 SRR493371
    ## ENSG00000186092         0
    ## ENSG00000279928         0
    ## ENSG00000279457        46
    ## ENSG00000278566         0
    ## ENSG00000273547         0
    ## ENSG00000187634       258

Making sure our row labels in colData match our column labels in
countData

``` r
rownames(colData)
```

    ## [1] "SRR493366" "SRR493367" "SRR493368" "SRR493369" "SRR493370" "SRR493371"

``` r
colnames(countData)
```

    ## [1] "SRR493366" "SRR493367" "SRR493368" "SRR493369" "SRR493370" "SRR493371"

``` r
all (rownames(colData) == colnames(countData))
```

    ## [1] TRUE

Removing zero-values from our dataset

``` r
# Identifying which points in the dataframe are zero values
zero.vals <- which(countData[,1:6]==0, arr.ind=TRUE)
head(zero.vals)
```

    ##                 row col
    ## ENSG00000186092   1   1
    ## ENSG00000279928   2   1
    ## ENSG00000278566   4   1
    ## ENSG00000273547   5   1
    ## ENSG00000237330  14   1
    ## ENSG00000162571  16   1

``` r
# Identifying rows with zero values
to.rm <- unique(zero.vals[,1])

# Removing the rows with zero values from our dataset
mycounts <- countData[-to.rm,] # new dataset: mycounts
head(mycounts)
```

    ##                 SRR493366 SRR493367 SRR493368 SRR493369 SRR493370
    ## ENSG00000279457        23        28        29        29        28
    ## ENSG00000187634       124       123       205       207       212
    ## ENSG00000188976      1637      1831      2383      1226      1326
    ## ENSG00000187961       120       153       180       236       255
    ## ENSG00000187583        24        48        65        44        48
    ## ENSG00000187642         4         9        16        14        16
    ##                 SRR493371
    ## ENSG00000279457        46
    ## ENSG00000187634       258
    ## ENSG00000188976      1504
    ## ENSG00000187961       357
    ## ENSG00000187583        64
    ## ENSG00000187642        16
