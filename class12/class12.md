Class 12 Structural Bioinformatics Part 2
================

## Preparing files for docking

Producing a protein-only PDB file and a drug-only PDB file

``` r
library(bio3d)
res <- read.pdb("all.pdbqt", multi=TRUE)
write.pdb(res, "results.pdb")
```

``` r
res <- read.pdb("all.pdbqt", multi=TRUE) 
ori <- read.pdb("ligand.pdbqt")
rmsd(ori, res)
```

    ##  [1]  0.590 11.163 10.531  4.364 11.040  3.682  5.741  3.864  5.442 10.920
    ## [11]  4.318  6.249 11.084  8.929

``` r
write.pdb(res, "results.pdb")
```

## Exploring the conformational dynamics of proteins through normal mode analysis (NMA)

### Viewing NMA results in R

``` r
pdb <- read.pdb("1HEL")
```

    ##   Note: Accessing on-line PDB file

``` r
modes <- nma(pdb) 
```

    ##  Building Hessian...     Done in 0.026 seconds.
    ##  Diagonalizing Hessian...    Done in 0.102 seconds.

``` r
plot(modes, sse=pdb)
```

![](class12_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

### Creating a results file to view in VMD

``` r
# Visualize NMA results
mktrj(modes, mode=7, file="nma_7.pdb")
```
