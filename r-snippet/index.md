# Initial
```{r}
install.packages("spAddins")
install.packages("remedy")
```

# Useful website

[rweekly](https://rweekly.org/)

[awesome-r](https://awesome-r.com/index.html)

[r-users_job](https://www.r-users.com/)

# Package 

### Repos

```{r}
options(repos = "http://cran.rstudio.org")
# options(repos = "https://cloud.r-project.org")
```
### Offline install package
```{}
install.packages(".../path/to/package.tar.gz", type="source", repos=NULL) 
```

# ggplot
## Awesome ggplot2
### Themes and aesthetics
- gghighlight{Eg: gghighlight(max(value) > 19)}
- ggsci {Eg: scale_color_palname(), scale_fill_palname()}
- ggfittext {Eg. geom_fit_text(reflow = TRUE, grow = TRUE)}
- hrbrtheme {Eg: scale_y_comma(), theme_ipsum_rc()}
- bbplot {https://bbc.github.io/rcookbook/, Eg: bbc_style(), finalise_plot()}
- ggthemr {https://github.com/cttobin/ggthemr}



### Presentation, composition and scales
- tagger

## format axis

- scale_y_continuous(label=scales::comma)
- scale_x_date(date_breaks = "2 month", date_labels = "%m-%Y")
- theme(legend.title = element_blank(),
        legend.position = "bottom",
        axis.text.x = element_text(angle = 30))

## format axis text


```{r}
theme(axis.text.x = element_text(size = 14), axis.title.x = element_text(size = 16),
      axis.text.y = element_text(size = 14), axis.title.y = element_text(size = 16),
      plot.title = element_text(size = 20, face = "bold", color = "darkgreen"))
      
theme(axis.ticks.length.y = unit(nc * 0.15,"cm"))
```
## geom_line with x is factor

```{r}
geom_line(aes(group = 1))
```

## combine graphs
`https://cran.r-project.org/web/packages/patchwork/vignettes/patchwork.html`

## vietnamese font

```{r}
Sys.setlocale(category = "LC_ALL", locale = "vietnamese")

eval(parse("R/graph_pqr_201911.R", encoding = "UTF-8"))

plot(1:4,rep(1,4), pch=c("\u0111","\u01B0","\u01A1","\u0103"),cex=4)
# Uppercase
plot(1:4,rep(1,4), pch=c("\U0110","\u01AF","\u01A0","\u0102"),cex=4)
```

# File

### edit file
```{r}
line="blah text blah blah etc etc"
write(line,file=paste0("vignettes/", ticker, ".Rmd"),append=TRUE)
```

# data.table
https://atrebas.github.io/post/2019-03-03-datatable-dplyr/

# dplyr

```r
# select na vars
fnc_na_vars <- function(x) {any(is.na(x))}
na_vars <- dt %>%
  select_if(fnc_na_vars) %>% 
  names() 
```

```{r}
group_by(xxx) %>% count()
```

```{r}
category <- enquo(category)	
p <- df %>% 
	group_by(!!category) %>% 
	summarise(cnt = n())

rlang::quo_text(category)

.var <- sym(.symbol)

```
## top_n_by function
```{r}
f_top_n <- function(df, n, top_by){
  top_by <- enquo(top_by)
  
  top_val <- df %>% 
    filter(is.finite(!!top_by)) %>% 
    pull(!!top_by) %>% 
    unique() %>% 
    sort(decreasing = TRUE) %>% 
    head(n) 
  
  filter(df, !!top_by %in% top_val) %>% return()
}

```

# lubridate

```{r}
x <- as.Date("2009-09-02")
wday(ymd(080101), label = TRUE, abbr = TRUE)
month(x)
year(x)
```


# zoo

```{r}
zoo::as.yearmon("Mar 2012", "%b %Y")
```


# file and folder

```{r}
r18_2017 <- Sys.glob(paste0(my_folder, "2017/*.xlsx"))

r18_2017 <- list.files(paste0(my_folder, "2017/"), full.names = T)

dt <- rio::import_list(r18_files, rbind = TRUE)
```


# string

## Bỏ dấu

```{r}
stringi::stri_trans_general('Nguyễn Ngọc Bình', "latin-ascii" )
```


# check slow code by **provis**

```{r}
## Generate data
times <- 4e5
cols <- 150
data <- as.data.frame(x = matrix(rnorm(times * cols, mean = 5), ncol = cols))
data <- cbind(id = paste0("g", seq_len(times)), data)

profvis::profvis({
  data1 <- data   # Store in another variable for this run

  ### Get column means
  means <- apply(data1[, names(data1) != "id"], 2, mean)

  ### Subtract mean from each column
  for (i in seq_along(means)) {
    data1[, names(data1) != "id"][, i] <- data1[, names(data1) != "id"][, i] - means[i]
  }
})
```


# purrr

## compose

```{r}
tidy_lm <- compose(tidy, lm)
tidy_lm(Sepal.Length ~ Species, data = iris)
```


## partial

```{r}
mean_na_rm <- partial(mean, na.rm = TRUE)
```

## reduce

```{r}
dfs <- list(
  age = tibble(name = "John", age = 30),
  sex = tibble(name = c("John", "Mary"), sex = c("M", "F")),
  trt = tibble(name = "Mary", treatment = "A")
)

dfs %>% reduce(full_join)
```

# Hàm xử lý outlier
```{r}
f_outlier <- function(x){
  threshold <- quantile(x, probs = c(0.005, 0.95), na.rm = TRUE, type = 3)
  
  y <- case_when(x > threshold[2] ~ threshold[2],
          x < threshold[1] ~ threshold[1],
          TRUE ~ x) 
  return(y)
}
```
# So sánh khác biệt giữa 2 file
```{r}
library(diffr)
diffr("D:/TMP/new 1.txt", "D:/TMP/new 2.txt", contextSize = 0, minJumpSize = 500)
```

# Optical Character Recognition (OCR)
```{r}
if(!require("tesseract")) {install.packages("tesseract")}
library(tesseract)
library(dplyr)
text <- ocr("D:/tmp/image2.png", engine = tesseract("eng"))
cat(text)
text %>% strsplit(split = "\n") %>% rio::export("x.xlsx")
```

# Markdown
## rpub
```{r, eval = F}
---
title: "Correlation analysis"
author: "Nguyễn Ngọc Bình"
date: "`r format(Sys.Date(),'%Y-%m-%d')`"
output:
  html_document:
    code_download: true
    code_folding: show
    number_sections: yes
    theme: "default"
    toc: TRUE
    toc_float: TRUE
    dev: 'svg'
editor_options:
  chunk_output_type: console
---
```
## image
`![](../figures/d_i_d_graph.png)
`

bookdown::html_document2, bookdown::word_document2
```{r}
![(\#fig:nnet2)Một mạng nơ-ron với bốn đầu vào và một lớp ẩn với ba nơ-ron ẩn.](images/nnet2.png)
\@ref(fig:nnet2)
```
or

```{r}
knitr::opts_chunk$set(echo = FALSE, fig.height = 5, fig.width = 7, out.width = "70%")
knitr::include_graphics("figures/d_i_d_graph.png")
```
### Format number in rmarkdown
``` fnc_kbl <- function(df) {
  df %>%
    mutate_if(
      is.numeric,
      format,
      digits = 2,
      nsmall = 2,
      big.mark = ".",
      decimal.mark = ","
    ) %>%
    kbl() %>%
    kable_classic(full_width = F)
}
```
### Format table in word
```{r}
fnc_print_tbl_df <- function(tbl_name) {
  out <- tbl_name %>%
    ungroup() %>% 
    mutate_if(is.numeric, round, 2) %>%
    flextable() %>%
    autofit() %>% 
    theme_zebra(odd_header = '#8064A2') %>% 
    font(fontname = 'Tahoma', part = 'all') %>% 
    fontsize(size = 10, part = 'all')%>% 
    border(border = officer::fp_border(color = "#8064A2")) 
  return(out)
}
```

### import data
```{r}
rio::import(xml2::xml2_example("cd_catalog.xml"))
```

### Reticulate 

```
file.edit(file.path("~", ".Rprofile"))
# RETICULATE_PYTHON="C/Users/nguye/anaconda3"
```
