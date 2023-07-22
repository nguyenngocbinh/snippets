---
title: reticulate
---

Install python in r step by step

### Create environment

```r
library(reticulate)
conda_create(envname = 'D:/python/env/r-reticulate', python_version = '3.6.13')
```

### Edit .Rprofile
```r
# usethis::edit_r_profile()
# Sys.setenv(RETICULATE_PYTHON = 'D:\\python\\env\\r-reticulate\\') # version 3.6
```

### Install python package

#### Default environment

```r
my_env <- "D:\\python\\envs\\r-reticulate"
```

#### Install packages using conda
```r
reticulate::conda_install(envname = my_env, packages = "lightgbm")
```

#### Install packages using pip

```r
reticulate::py_install(packages = "xgboost", envname = my_env)
```

### Extra
#### install miniconda if needed
```r
reticulate::install_miniconda(path = "D:/python/")
reticulate::miniconda_update(path = "D:/python/") # update if needed
```

#### check python version
```r
reticulate::py_version()
reticulate::py_versions_windows()
```

#### check config
```r
reticulate::py_config() 
reticulate::py_discover_config()
```

#### check conda envs
```r
reticulate::conda_list()
# conda_remove("pillow")
reticulate::virtualenv_list()
```

#### convert to rmd
```r
rmarkdown:::convert_ipynb("python/volatility-prediction.ipynb")
```
