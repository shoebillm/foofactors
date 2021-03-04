
<!-- README.md is generated from README.Rmd. Please edit that file -->

**NOTE: This is a toy package created for expository purposes, for the
second edition of [R Packages](https://r-pkgs.org). It is not meant to
actually be useful. If you want a package for factor handling, please
see [forcats](https://forcats.tidyverse.org).**

# foofactors

<!-- badges: start -->

<!-- badges: end -->

Factors are a very useful type of variable in R, but they can also be
very aggravating. This package provides some helper functions for the
care and feeding of factors.

## Installation

You can install foofactors like so:

``` r
devtools::install_github("shoebillm/foofactors")
#> Downloading GitHub repo shoebillm/foofactors@HEAD
#> crayon    (1.3.4 -> 1.4.1) [CRAN]
#> cli       (2.2.0 -> 2.3.1) [CRAN]
#> pillar    (1.4.7 -> 1.5.0) [CRAN]
#> lifecycle (0.2.0 -> 1.0.0) [CRAN]
#> tibble    (3.0.5 -> 3.1.0) [CRAN]
#> forcats   (0.5.0 -> 0.5.1) [CRAN]
#> Installing 6 packages: crayon, cli, pillar, lifecycle, tibble, forcats
#> 
#> The downloaded binary packages are in
#>  /var/folders/k5/1lsn5p5924v3wcq3xbfg9qlh0000gn/T//Rtmpf3zp2G/downloaded_packages
#>      checking for file ‘/private/var/folders/k5/1lsn5p5924v3wcq3xbfg9qlh0000gn/T/Rtmpf3zp2G/remotes51fc71fe4e66/shoebillm-foofactors-5666eee/DESCRIPTION’ ...  ✓  checking for file ‘/private/var/folders/k5/1lsn5p5924v3wcq3xbfg9qlh0000gn/T/Rtmpf3zp2G/remotes51fc71fe4e66/shoebillm-foofactors-5666eee/DESCRIPTION’
#>   ─  preparing ‘foofactors’:
#>      checking DESCRIPTION meta-information ...  ✓  checking DESCRIPTION meta-information
#>   ─  checking for LF line-endings in source and make files and shell scripts
#>   ─  checking for empty or unneeded directories
#>   ─  building ‘foofactors_0.0.0.9000.tar.gz’
#>      
#> 
```

## Example

Binding two factors via `fbind()`:

``` r
library(foofactors)
a <- factor(c("character", "hits", "your", "eyeballs"))
b <- factor(c("but", "integer", "where it", "counts"))
```

Simply catenating two factors leads to a result that most don’t expect.

``` r
c(a, b)
#> [1] 1 3 4 2 1 3 4 2
```

The `fbind()` function glues two factors together and returns factor.

``` r
fbind(a, b)
#> [1] character hits      your      eyeballs  but       integer   where it 
#> [8] counts   
#> Levels: but character counts eyeballs hits integer where it your
```

Often we want a table of frequencies for the levels of a factor. The
base `table()` function returns an object of class `table`, which can be
inconvenient for downstream work.

``` r
set.seed(1234)
x <- factor(sample(letters[1:5], size = 100, replace = TRUE))
table(x)
#> x
#>  a  b  c  d  e 
#> 19 19 21 22 19
```

The `fcount()` function returns a frequency table as a tibble with a
column of factor levels and another of frequencies:

``` r
fcount(x)
#> # A tibble: 5 x 2
#>   f         n
#>   <fct> <int>
#> 1 d        22
#> 2 c        21
#> 3 a        19
#> 4 b        19
#> 5 e        19
```
