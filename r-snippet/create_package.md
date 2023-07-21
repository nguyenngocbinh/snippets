---
title: Hướng dẫn tạo package trên R
---


### Cài đặt những packages cần thiết

```r
install.packages(c("devtools", "roxygen2", "testthat", "knitr", "usethis"))
```


### Tạo package mới

```r
usethis::create_package("D:/R/how.to.create.package")
```
Sau khi dùng lệnh này thì 1 project được tạo ra gồm:

- folder: R dùng để lưu tất cả các hàm 

- file: DESCRIPTION và NAMESPACE: 2 file này dùng để mô tả về package và dependencies 

### Một làm ví dụ

```r
# R/performance.R
# Sensitivity
#' @title sensitivity
#' @description Calculate the sensitivity for a given logit model.
#' @details For a given binary response actuals and predicted probability scores, sensitivity is defined as number of observations with the event AND predicted to have the event divided by the number of observations with the event. It can be used as an indicator to gauge how sensitive is your model in detecting the occurence of events, especially when you are not so concerned about predicting the non-events as true.
#' @author Selva Prabhakaran \email{selva86@@gmail.com}
#' @export sensitivity
#' @param actuals The actual binary flags for the response variable. It can take a numeric vector containing values of either 1 or 0, where 1 represents the 'Good' or 'Events' while 0 represents 'Bad' or 'Non-Events'.
#' @param predictedScores The prediction probability scores for each observation. If your classification model gives the 1/0 predcitions, convert it to a numeric vector of 1's and 0's.
#' @param threshold If predicted value is above the threshold, it will be considered as an event (1), else it will be a non-event (0). Defaults to 0.5.
#' @return The sensitivity of the given binary response actuals and predicted probability scores, which is, the number of observations with the event AND predicted to have the event divided by the nummber of observations with the event.
#' @examples
#' data('ActualsAndScores')
#' sensitivity(actuals=ActualsAndScores$Actuals, predictedScores=ActualsAndScores$PredictedScores)
sensitivity <- function(actuals, predictedScores, threshold = 0.5) {
  predicted_dir <- ifelse(predictedScores < threshold, 0, 1)
  actual_dir <- actuals
  no_with_and_predicted_to_have_event <- sum(actual_dir == 1 & predicted_dir == 1, na.rm = T)
  no_with_event <- sum(actual_dir == 1, na.rm = T)
  return(no_with_and_predicted_to_have_event/no_with_event)
}
```


### Chỉnh sửa DESCRIPTION

- Chỉnh sửa thông tin như tác giả, đồng tác giả, email, License, mô tả tổng quát về package ...
- Thêm thông tin DESCRIPTION

```r
usethis::use_package('ggplot2', type = 'import', min_version = TRUE)
usethis::use_package('scorecard', type = 'suggests', min_version = TRUE)

lapply(c('dplyr','ggplot2', 'pROC', 'ROCR', 'tidyr', 'purrr', 'magrittr', 'tibble', 'knitr'),
       function(pkg) usethis::use_package(pkg, type = 'suggests', min_version = TRUE))
```


### Chỉnh sửa NAMESPACE 

- Tạo RD file

- Sau khi sử dụng lệnh này thì sẽ có folder man được tạo ra, folder này chứa các hướng dẫn sử dụng các hàm trong package

```r
devtools::document()
roxygen2::roxygenise() # cách khác
```

### Thêm hướng dẫn sử dụng (vignettes)

```r
devtools::clean_vignettes() # NOTE: backup data before run these commands
usethis::use_vignette("mba_past")
```
- build vignettes

```r
devtools::build_vignettes()
```

- Sau khi sử dụng lệnh này thì sẽ có thêm folder `doc` chứa `Rcode` và các file đã được knit

### Thêm data vào package

- Với dữ liệu nhỏ < 1Mb thì có thể thêm luôn vào package

```r
hmeq <- read.csv('D:/tmp/hmeq-data/hmeq.csv')
names(hmeq) <- tolower(names(hmeq))
usethis::use_data_raw("hmeq")
usethis::use_data(hmeq)

#' hmeq
#' @docType data
#' @name hmeq
#' @usage data(hmeq)
#' @author Nguyen Ngoc Binh \email{nguyenngocbinhneu@@gmail.com}
#' @references \url{https://codeload.github.com/Carl-Lejerskar/HMEQ/zip/master}
#' @keywords datasets
#' @examples
#' data(hmeq)
NULL
```

### Build package

```r
devtools::check()
devtools::build()
```
