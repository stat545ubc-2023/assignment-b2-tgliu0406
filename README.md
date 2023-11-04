
<!-- README.md is generated from README.Rmd. Please edit that file -->

# countMissing

<!-- badges: start -->
<!-- badges: end -->

Given a data frame `data` and a column `group`,
`count_all_missing_by_group()` creates a new data frame with one row per
level of `group`. The first column of the output data frame contains the
levels of `group`, and the rest of the columns contain the number of
missing values for all columns in `data` except `group`.

## Installation

You can install the development version of countMissing from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("stat545ubc-2023/countMissing")
#> Downloading GitHub repo stat545ubc-2023/countMissing@HEAD
#> ── R CMD build ─────────────────────────────────────────────────────────────────
#>          checking for file 'C:\Users\Tiange\AppData\Local\Temp\RtmpQ71wC6\remotes2218234f4d11\stat545ubc-2023-countMissing-1cb47ce/DESCRIPTION' ...  ✔  checking for file 'C:\Users\Tiange\AppData\Local\Temp\RtmpQ71wC6\remotes2218234f4d11\stat545ubc-2023-countMissing-1cb47ce/DESCRIPTION' (355ms)
#>       ─  preparing 'countMissing':
#>    checking DESCRIPTION meta-information ...     checking DESCRIPTION meta-information ...   ✔  checking DESCRIPTION meta-information
#>       ─  excluding invalid files
#>    Subdirectory 'R' contains invalid file names:
#>      'assignment-b2-prebake.Rmd'
#>       ─  checking for LF line-endings in source and make files and shell scripts
#>   ─  checking for empty or unneeded directories
#>       ─  building 'countMissing_0.0.0.9000.tar.gz'
#>      
#> 
#> 将程序包安装入'C:/Users/Tiange/AppData/Local/Temp/Rtmpycar7Q/temp_libpath573c1f6745cb'
#> (因为'lib'没有被指定)
```

## Example

This is a basic example which shows you how to solve a common problem:

``` r
library(countMissing)
## countMissing relies on tidyverse
library(tidyverse)
#> ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
#> ✔ ggplot2 3.3.6     ✔ purrr   0.3.4
#> ✔ tibble  3.1.8     ✔ dplyr   1.0.9
#> ✔ tidyr   1.2.0     ✔ stringr 1.5.0
#> ✔ readr   2.1.2     ✔ forcats 0.5.1
#> Warning: 程辑包'ggplot2'是用R版本4.2.2 来建造的
#> Warning: 程辑包'stringr'是用R版本4.2.3 来建造的
#> ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
#> ✖ dplyr::filter() masks stats::filter()
#> ✖ dplyr::lag()    masks stats::lag()
## load the dataset for the following demo
library(palmerpenguins)
#> Warning: 程辑包'palmerpenguins'是用R版本4.2.3 来建造的
```

This example computes the number of missing values in the `airquality`
dataset grouped by the `cyl` column.

``` r
count_all_missing_by_group(airquality, Month)
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

This example has the same output as the last example, but shows off an
alternative way of invoking the `count_all_missing_by_group()`: piping
the dataset into the function.

``` r
airquality |> count_all_missing_by_group(Month) 
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

The optional `.groups` argument allows us to keep the output grouped by
the grouping column. See example below; notice how the output is a
grouped tibble, rather than the ungrouped tibble output of the earlier
examples.

``` r
count_all_missing_by_group(airquality, Month, .groups = "keep")
#> # A tibble: 5 × 6
#> # Groups:   Month [5]
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```
