---
title: file and folder
---

```r
r18_2017 <- Sys.glob(paste0(my_folder, "2017/*.xlsx"))

r18_2017 <- list.files(paste0(my_folder, "2017/"), full.names = T)

dt <- rio::import_list(r18_files, rbind = TRUE)
```

