Data Visualization: A Practical Introduction
================
Last updated in August 2020

## Preface

This repository provides datasets, code, and plots as shown in Kieran
Healy’s book, which is freely accessible at <https://socviz.co>. If
datasets used are not readily usable and required some modification
before plotting, code for cleaning the data is also available here. You
can access all these data in the folder `data` where I provide the raw
and cleaned datasets for future use.

I use the Rmarkdown file provided by the author for taking notes while
reading the book. This document will not be completely identical to the
book itself since I sometimes add my own code and notes to add clarity
for myself.

``` r
knitr::opts_chunk$set(
    echo = TRUE,
    fig.align = "center",
    message = FALSE,
    warning = FALSE,
    comment = "",
    dpi = 300,
    fig.width = 8,
    fig.height = 5
)
```

## Data Visualization Notes

This is a starter RMarkdown template to accompany *Data Visualization*
(Princeton University Press, 2019). You can use it to take notes, write
your code, and produce a good-looking, reproducible document that
records the work you have done. At the very top of the file is a section
of *metadata*, or information about what the file is and what it does.
The metadata is delimited by three dashes at the start and another three
at the end. You should change the title, author, and date to the values
that suit you. Keep the `output` line as it is for now, however. Each
line in the metadata has a structure. First the *key* (“title”,
“author”, etc), then a colon, and then the *value* associated with
the key.

## This is an RMarkdown File

Markdown is a simple formatting syntax for authoring HTML, PDF, and MS
Word documents. For more details on using R Markdown see
<http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. A *code chunk* is a specially delimited
section of the file. You can add one by moving the cursor to a blank
line choosing Code \> Insert Chunk from the RStudio menu. When you do,
an empty chunk will appear (without the hashes):

```` r
# ```{r}
# 
# ```
````

Code chunks are delimited by three backticks (found to the left of the 1
key on US and UK keyboards) at the start and end. The opening backticks
also have a pair of braces and the letter `r`, to indicate what language
the chunk is written in. You write your code inside the code chunks.
Write your notes and other material around them, as here.

## Before you Begin

To install the tidyverse, make sure you have an Internet connection.
Then *manually* run the code in the chunk below. If you knit the
document if will be skipped. We do this because you only need to install
these packages once, not every time you run this file. Either knit the
chunk using the little green “play” arrow to the right of the chunk
area, or copy and paste the text into the console window.

``` r
## This code will not be evaluated automatically.
## (Notice the eval = FALSE declaration in the options section of the
## code chunk)

my_packages <- c("tidyverse", "broom", "coefplot", "cowplot",
                 "gapminder", "GGally", "ggrepel", "ggridges", "gridExtra",
                 "here", "interplot", "margins", "maps", "mapproj",
                 "mapdata", "MASS", "quantreg", "rlang", "scales",
                 "survey", "srvyr", "viridis", "viridisLite", "devtools")

install.packages(my_packages, repos = "http://cran.rstudio.com")
```

## Set Up Your Project and Load Libraries

To begin we must load some libraries we will be using. If we do not load
them, R will not be able to find the functions contained in these
libraries. The tidyverse includes ggplot and other tools. We also load
the socviz and gapminder libraries.

``` r
## By defult, show code for all chunks in the knitted document,
## as well as the output. To override for a particular chunk
## use echo = FALSE in its options.
# knitr::opts_chunk$set(echo = TRUE) 

## Set the default size of figures
# knitr::opts_chunk$set(fig.width=8, fig.height=5)  

## Load the libraries we will be using
library(gapminder) # Dataset `gapminder`
library(here)      # Navigate files
library(socviz)    # Package specific to this book (datasets, other tools)
library(tidyverse) # Manipulate and visualise data
library(knitr)     # Tidy outputs
```

Notice that here, the braces at the start of the code chunk have some
additional options set in them. There is the language, `r`, as before.
This is required. Then there is the word `setup`, which is a label for
your code chunk. Labels are useful to briefly say what the chunk does.
Label names must be unique (no two chunks in the same document can have
the same label) and cannot contain spaces. Then, after the comma, an
option is set: `include=FALSE`. This tells R to run this code but not to
include the output in the final document.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. You can embed an R code chunk like this:

``` r
gapminder
```

    # A tibble: 1,704 x 6
       country     continent  year lifeExp      pop gdpPercap
       <fct>       <fct>     <int>   <dbl>    <int>     <dbl>
     1 Afghanistan Asia       1952    28.8  8425333      779.
     2 Afghanistan Asia       1957    30.3  9240934      821.
     3 Afghanistan Asia       1962    32.0 10267083      853.
     4 Afghanistan Asia       1967    34.0 11537966      836.
     5 Afghanistan Asia       1972    36.1 13079460      740.
     6 Afghanistan Asia       1977    38.4 14880372      786.
     7 Afghanistan Asia       1982    39.9 12881816      978.
     8 Afghanistan Asia       1987    40.8 13867957      852.
     9 Afghanistan Asia       1992    41.7 16317921      649.
    10 Afghanistan Asia       1997    41.8 22227415      635.
    # … with 1,694 more rows

The remainder of this document contains the chapter headings for the
book, and an empty code chunk in each section to get you started. Try
knitting this document now by clicking the “Knit” button in the RStudio
toolbar, or choosing File \> Knit Document from the RStudio menu.

## Look at Data

``` r
# Inspect the data (the raw data are readily available from R)
kable(anscombe)
```

| x1 | x2 | x3 | x4 |    y1 |   y2 |    y3 |    y4 |
| -: | -: | -: | -: | ----: | ---: | ----: | ----: |
| 10 | 10 | 10 |  8 |  8.04 | 9.14 |  7.46 |  6.58 |
|  8 |  8 |  8 |  8 |  6.95 | 8.14 |  6.77 |  5.76 |
| 13 | 13 | 13 |  8 |  7.58 | 8.74 | 12.74 |  7.71 |
|  9 |  9 |  9 |  8 |  8.81 | 8.77 |  7.11 |  8.84 |
| 11 | 11 | 11 |  8 |  8.33 | 9.26 |  7.81 |  8.47 |
| 14 | 14 | 14 |  8 |  9.96 | 8.10 |  8.84 |  7.04 |
|  6 |  6 |  6 |  8 |  7.24 | 6.13 |  6.08 |  5.25 |
|  4 |  4 |  4 | 19 |  4.26 | 3.10 |  5.39 | 12.50 |
| 12 | 12 | 12 |  8 | 10.84 | 9.13 |  8.15 |  5.56 |
|  7 |  7 |  7 |  8 |  4.82 | 7.26 |  6.42 |  7.91 |
|  5 |  5 |  5 |  8 |  5.68 | 4.74 |  5.73 |  6.89 |

``` r
# Wrangle data
anscombe_cleaned <- anscombe %>% 
  # Add unique identifier per observation
  mutate(id = rownames(anscombe)) %>% 
  
  # Wide to long format
  pivot_longer(cols = c(starts_with("x"), starts_with("y")),
               names_to = "variable",
               values_to = "value") %>% 
  
  # Text parsing
  transmute(
    id = id,
    plot = str_sub(string = variable, start = 2, end = 2),
    axis = str_sub(string = variable, start = 1, end = 1),
    value = value
  ) %>% 
  
  # Long to wide format
  pivot_wider(names_from = axis, values_from = value)

# Inspect the cleaned data
head(anscombe_cleaned) %>% # Show the first six observations
  kable()
```

| id | plot |  x |    y |
| :- | :--- | -: | ---: |
| 1  | 1    | 10 | 8.04 |
| 1  | 2    | 10 | 9.14 |
| 1  | 3    | 10 | 7.46 |
| 1  | 4    |  8 | 6.58 |
| 2  | 1    |  8 | 6.95 |
| 2  | 2    |  8 | 8.14 |

``` r
# Save the cleaned and raw datasets
write_rds(anscombe_cleaned, path = here("data", "anscombe_cleaned.rds"))
write_rds(anscombe, path = here("data", "anscombe_raw.rds"))

# Reproduce plots, with slight modification
anscombe_cleaned %>% 
  ggplot(aes(x = x, y = y)) +
    geom_point() +
    geom_smooth(formula = "y ~ x", method = "lm", se = FALSE, colour = "blue3") +
    facet_wrap(~plot) +
    theme_bw() +
    theme(aspect.ratio = 1,
          panel.grid.minor = element_blank(),
          plot.title = element_text(hjust = 0.5),
          plot.subtitle = element_text(hjust = 0.5),
          legend.position = "none") +
    labs(x = "x values",
         y = "y values",
         caption = "Figure 1.1",
         title = "\nPlots of Anscombe's quartet",
         subtitle = "All have a correlation coefficient of 0.81")
```

<img src="README_files/figure-gfm/unnamed-chunk-1-1.png" style="display: block; margin: auto;" />

``` r
# Save the resulting graphic
ggsave(filename = "figure-1.1.png",
       path = here("graphics"))
```

## Get Started

## Make a Plot

## Show the Right Numbers

## Graph Tables, Make Labels, Add Notes

## Work with Models

## Draw Maps

## Refine your Plots

## Appendix

``` r
sessionInfo()
```

``` 
R version 4.0.1 (2020-06-06)
Platform: x86_64-apple-darwin17.0 (64-bit)
Running under: macOS Catalina 10.15.5

Matrix products: default
BLAS:   /Library/Frameworks/R.framework/Versions/4.0/Resources/lib/libRblas.dylib
LAPACK: /Library/Frameworks/R.framework/Versions/4.0/Resources/lib/libRlapack.dylib

locale:
[1] en_GB.UTF-8/en_GB.UTF-8/en_GB.UTF-8/C/en_GB.UTF-8/en_GB.UTF-8

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
 [1] knitr_1.28      forcats_0.5.0   stringr_1.4.0   dplyr_1.0.1    
 [5] purrr_0.3.4     readr_1.3.1     tidyr_1.1.0     tibble_3.0.3   
 [9] ggplot2_3.3.2   tidyverse_1.3.0 socviz_1.2      here_0.1       
[13] gapminder_0.3.0

loaded via a namespace (and not attached):
 [1] Rcpp_1.0.5       lubridate_1.7.9  lattice_0.20-41  assertthat_0.2.1
 [5] rprojroot_1.3-2  digest_0.6.25    utf8_1.1.4       R6_2.4.1        
 [9] cellranger_1.1.0 backports_1.1.8  reprex_0.3.0     evaluate_0.14   
[13] httr_1.4.1       highr_0.8        pillar_1.4.6     rlang_0.4.7     
[17] readxl_1.3.1     rstudioapi_0.11  blob_1.2.1       Matrix_1.2-18   
[21] rmarkdown_2.3    labeling_0.3     splines_4.0.1    munsell_0.5.0   
[25] broom_0.7.0      compiler_4.0.1   modelr_0.1.8     xfun_0.15       
[29] pkgconfig_2.0.3  mgcv_1.8-31      htmltools_0.5.0  tidyselect_1.1.0
[33] fansi_0.4.1      crayon_1.3.4     dbplyr_1.4.4     withr_2.2.0     
[37] grid_4.0.1       nlme_3.1-148     jsonlite_1.6.1   gtable_0.3.0    
[41] lifecycle_0.2.0  DBI_1.1.0        magrittr_1.5     scales_1.1.1    
[45] cli_2.0.2        stringi_1.4.6    farver_2.0.3     fs_1.5.0        
[49] xml2_1.3.2       ellipsis_0.3.1   generics_0.0.2   vctrs_0.3.2     
[53] tools_4.0.1      glue_1.4.1       hms_0.5.3        yaml_2.2.1      
[57] colorspace_1.4-1 rvest_0.3.5      haven_2.3.1     
```
