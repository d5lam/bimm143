Class 11: Structural Bioinformatics Part 1
================

## The PDB database for biomolecular structural data

> Q1: Determine the percentage of structures solved by X-Ray and
> Electron Microscopy.

``` r
methods <- read.csv("Data Export Summary.csv")
methods
```

    ##   Experimental.Method Proteins Nucleic.Acids Protein.NA.Complex Other
    ## 1               X-Ray   131278          2059               6759     8
    ## 2                 NMR    11235          1303                261     8
    ## 3 Electron Microscopy     2899            32                999     0
    ## 4               Other      280             4                  6    13
    ## 5        Multi Method      144             5                  2     1
    ##    Total
    ## 1 140104
    ## 2  12807
    ## 3   3930
    ## 4    303
    ## 5    152

``` r
# Determining percent of structures solved by X-Ray and EM
total <- sum(methods$Total)
total # Calculating total
```

    ## [1] 157296

``` r
xray_em <- sum(methods[1,6], methods[3,6])

round(xray_em/total * 100, 2) # Calculating proportion of structures solved by X-Ray and EM
```

    ## [1] 91.57

> Determine what proportion of structures are proteins.

``` r
round (sum(methods$Proteins) / sum(methods$Total) * 100, 2)
```

    ## [1] 92.71

## HIV-Pr structure analysis

> Loading in bio3D

``` r
library(bio3d)
```

> Reading in 1HSG

``` r
read.pdb("1HSG")
```

    ##   Note: Accessing on-line PDB file

    ## 
    ##  Call:  read.pdb(file = "1HSG")
    ## 
    ##    Total Models#: 1
    ##      Total Atoms#: 1686,  XYZs#: 5058  Chains#: 2  (values: A B)
    ## 
    ##      Protein Atoms#: 1514  (residues/Calpha atoms#: 198)
    ##      Nucleic acid Atoms#: 0  (residues/phosphate atoms#: 0)
    ## 
    ##      Non-protein/nucleic Atoms#: 172  (residues: 128)
    ##      Non-protein/nucleic resid values: [ HOH (127), MK1 (1) ]
    ## 
    ##    Protein sequence:
    ##       PQITLWQRPLVTIKIGGQLKEALLDTGADDTVLEEMSLPGRWKPKMIGGIGGFIKVRQYD
    ##       QILIEICGHKAIGTVLVGPTPVNIIGRNLLTQIGCTLNFPQITLWQRPLVTIKIGGQLKE
    ##       ALLDTGADDTVLEEMSLPGRWKPKMIGGIGGFIKVRQYDQILIEICGHKAIGTVLVGPTP
    ##       VNIIGRNLLTQIGCTLNF
    ## 
    ## + attr: atom, xyz, seqres, helix, sheet,
    ##         calpha, remark, call
