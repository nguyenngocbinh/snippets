---
title: dplyr
---

## dplyr with bang bang example

### Varying the name of the output variable

We need to do the following:

- Use quo_name() to convert the input expression to string
- Use := helper provided by rlang

```r
# https://www.onceupondata.com/2017/08/12/my-first-steps-into-the-world-of-tidyeval/
add_tag_count <- function(x, cname, count_col){
  
  cname <- enquo(cname)
  
  count_col <- enquo(count_col)
  count_col_name <- quo_name(count_col)

  x %>% 
    mutate(!!count_col_name := map_int(!!cname, length))
}
```

### Capturing multiple variables

```r
freq_tbl <- function(df, ..., percent = TRUE){
  group <- quos(...)
  
  out <- df %>% 
    group_by(!!!group) %>% 
    summarise(freq = n()) %>% 
    arrange(desc(freq)) %>% 
    ungroup()
  
  if(percent == TRUE){
    out <- out %>% 
      mutate(percentage = 100*freq/sum(freq))
  }
  return(out)
}
```

## References

- [tidyeval](https://www.onceupondata.com/2017/08/12/my-first-steps-into-the-world-of-tidyeval/)