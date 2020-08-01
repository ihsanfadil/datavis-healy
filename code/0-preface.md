Preface
================
Last updated: August 2020

## Install required packages

``` r
my_packages <- c("tidyverse", "broom", "coefplot", "cowplot",
                 "gapminder", "GGally", "ggrepel", "ggridges", "gridExtra",
                 "here", "interplot", "margins", "maps", "mapproj",
                 "mapdata", "MASS", "quantreg", "rlang", "scales",
                 "survey", "srvyr", "viridis", "viridisLite", "devtools")

install.packages(my_packages, repos = "http://cran.rstudio.com")
```

``` 

The downloaded binary packages are in
    /var/folders/gw/g95f62ld37g0wlrvpmwds3_w0000gn/T//RtmpjwdJhf/downloaded_packages
```

``` r
devtools::install_github("kjhealy/socviz")
```

``` 
vctrs (0.3.1 -> 0.3.2) [CRAN]
fs    (1.4.1 -> 1.5.0) [CRAN]
dplyr (1.0.0 -> 1.0.1) [CRAN]

  There are binary versions available but the source versions are later:
      binary source needs_compilation
fs     1.4.2  1.5.0              TRUE
dplyr  1.0.0  1.0.1              TRUE


The downloaded binary packages are in
    /var/folders/gw/g95f62ld37g0wlrvpmwds3_w0000gn/T//RtmpjwdJhf/downloaded_packages
     checking for file ‘/private/var/folders/gw/g95f62ld37g0wlrvpmwds3_w0000gn/T/RtmpjwdJhf/remotesb71c73d441d9/kjhealy-socviz-eca8021/DESCRIPTION’ ...  ✓  checking for file ‘/private/var/folders/gw/g95f62ld37g0wlrvpmwds3_w0000gn/T/RtmpjwdJhf/remotesb71c73d441d9/kjhealy-socviz-eca8021/DESCRIPTION’
  ─  preparing ‘socviz’:
     checking DESCRIPTION meta-information ...  ✓  checking DESCRIPTION meta-information
  ─  checking for LF line-endings in source and make files and shell scripts
  ─  checking for empty or unneeded directories
  ─  building ‘socviz_1.2.tar.gz’
     
```
