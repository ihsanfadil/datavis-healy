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
    /var/folders/gw/g95f62ld37g0wlrvpmwds3_w0000gn/T//RtmpKXVu5B/downloaded_packages
```

``` r
devtools::install_github("kjhealy/socviz")
```

## Appendix

``` r
sessionInfo()
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
    
    loaded via a namespace (and not attached):
     [1] knitr_1.28        magrittr_1.5      usethis_1.6.1     devtools_2.3.1   
     [5] pkgload_1.1.0     R6_2.4.1          rlang_0.4.7       fansi_0.4.1      
     [9] stringr_1.4.0     tools_4.0.1       pkgbuild_1.1.0    xfun_0.15        
    [13] sessioninfo_1.1.1 cli_2.0.2         withr_2.2.0       remotes_2.2.0    
    [17] htmltools_0.5.0   ellipsis_0.3.1    yaml_2.2.1        assertthat_0.2.1 
    [21] digest_0.6.25     rprojroot_1.3-2   crayon_1.3.4      processx_3.4.3   
    [25] callr_3.4.3       fs_1.5.0          ps_1.3.3          curl_4.3         
    [29] testthat_2.3.2    memoise_1.1.0     glue_1.4.1        evaluate_0.14    
    [33] rmarkdown_2.3     stringi_1.4.6     compiler_4.0.1    backports_1.1.8  
    [37] desc_1.2.0        prettyunits_1.1.1
