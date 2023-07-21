---
title: ggplot2
---

### Pie chart
Pie chart with other approach this by defining another variable (call pos) in df that calculates the position of text labels. 
```r
# https://stackoverflow.com/questions/24803460/r-ggplot2-add-labels-on-facet-pie-chart
library(dplyr)
library(ggplot2)

df <- df %>% group_by(year) %>% mutate(pos = cumsum(quantity)- quantity/2)

ggplot(data=df, aes(x=factor(1), y=quantity, fill=factor(prod))) +
  geom_bar(stat="identity") +
  geom_text(aes(x= factor(1), y=pos, label = quantity), size=10) +  # note y = pos
  facet_grid(facets = .~year, labeller = label_value) +
  coord_polar(theta = "y")
```

# Donut chart
```r
count.data <- data.frame(
  class = c("1st", "2nd", "3rd", "Crew"),
  n = c(325, 285, 706, 885),
  prop = c(14.8, 12.9, 32.1, 40.2)
)
count.data

# Add label position
count.data <- count.data %>%
  arrange(desc(class)) %>%
  mutate(lab.ypos = cumsum(prop) - 0.5*prop)
count.data

mycols <- c("#0073C2FF", "#EFC000FF", "#868686FF", "#CD534CFF")

ggplot(count.data, aes(x = "", y = prop, fill = class)) +
  geom_bar(width = 1, stat = "identity", color = "white") +
  coord_polar("y", start = 0)+
  geom_text(aes(y = lab.ypos, label = prop), color = "white")+
  scale_fill_manual(values = mycols) +
  theme_void()

# Donut chart
ggplot(count.data, aes(x = 2, y = prop, fill = class)) +
  geom_bar(stat = "identity", color = "white") +
  coord_polar(theta = "y", start = 0)+
  geom_text(aes(y = lab.ypos, label = prop), color = "white")+
  scale_fill_manual(values = mycols) +
  theme_void()+
  xlim(0.5, 2.5)
```

### gganimate .gif
```
https://github.com/thomasp85/gganimate
```

### hrbrtheme

- format date

```r
scale_y_continuous(label=scales::comma)+
  scale_x_date(date_breaks = "2 month",
               date_labels = "%m-%Y")+
  theme(legend.title = element_blank(),
        legend.position = "bottom",
        axis.text.x = element_text(angle = 30))
```
- histogram

```r
ggplot(aes(x = cnt))+
  geom_histogram(bins = 18)+ # bins = 24
  labs(title = "Tong thoi gian",
       subtitle = "don vi",
       x = "So luong",
       y = "So quan sat")+
  scale_y_comma()+
  theme_ipsum_rc()+
  facet_wrap(~ bi_card_group, nrow = 2)
```

- theme

```r
theme(axis.text.x = element_text(size = 14), axis.title.x = element_text(size = 16),
      axis.text.y = element_text(size = 14), axis.title.y = element_text(size = 16),
      plot.title = element_text(size = 20, face = "bold", color = "darkgreen"))
```

### vietnamese text

```
plot(1:4,rep(1,4),pch=c("\u0111","\u01B0","\u01A1","\u0103"),cex=4)
```

### Area plot
```r
mu <- wdata %>%
  group_by(sex) %>%
  summarise(grp.mean = mean(weight))

# Area plot
a <- ggplot(economics, aes(x=date)) +
  geom_area(aes(y=psavert), fill = "#999999",
            color = "#999999", alpha=0.5) +
  geom_area(aes(y=uempmed), fill = "#E69F00",
            color = "#E69F00", alpha=0.5) +
  theme_minimal()

a + geom_density(aes(color = sex), alpha=0.4)+
  geom_vline(data = mu, aes(xintercept = grp.mean, color=sex),
             linetype="dashed")
```


### Density

```r
a + geom_density(aes(color = sex), alpha=0.4)+
  geom_vline(data = mu, aes(xintercept = grp.mean, color=sex),
             linetype="dashed")
```

### Histogram
```r
# Basic plot
a + geom_histogram()
# Change the number of bins
a + geom_histogram(bins = 50)
# Position adjustment: "identity" (overlaid)
a + geom_histogram(aes(color = sex), fill = "white", alpha = 0.6,
                   position="identity")
```


### Histogram with density plot
```r
# Color by groups
a + geom_histogram(aes(y=..density.., color = sex, fill = sex),
                   alpha=0.5, position="identity")+
  geom_density(aes(color = sex), size = 1)
```


### Box plot with mean points
```r
e + geom_boxplot() +
  stat_summary(fun.y = mean, geom = "point",
               shape = 18, size = 4, color = "blue")
```

### Change the default order of items
```r
e + geom_boxplot() +
  scale_x_discrete(limits=c("2", "0.5", "1"))
```
### Add mean points +/- SD
```r
# Use geom = "pointrange" or geom = "crossbar"
e + geom_violin(trim = FALSE) +
  stat_summary(fun.data="mean_sdl", fun.args = list(mult=1),
               geom="pointrange", color = "red")
# Combine with box plot to add median and quartiles
e + geom_violin(trim = FALSE) +
  geom_boxplot(width = 0.2)
```

### geom_line
```r
# Change line types, point shapes and colors
p + geom_line(aes(linetype=supp, color = supp))+
  geom_point(aes(shape=supp, color = supp))
```


### geom_bar with labels
```r
require(plyr)
# Sort by dose and supp
df_sorted <- arrange(df2, dose, supp)

# Calculate the cumulative sum of len for each dose
df_cumsum <- ddply(df_sorted, "dose", transform,
                   label_ypos=cumsum(len))

# Create the bar plot
ggplot(data=df_cumsum, aes(x = dose, y = len, fill = supp)) +
  geom_bar(stat = "identity")+
  geom_text(aes(y = label_ypos, label = len), vjust=1.6,
            color = "white", size = 3.5)
```


### Pie charts
```r
# Basic pie charts
df <- data.frame(
  group = c("Male", "Female", "Child"),
  value = c(25, 25, 50))

p <- ggplot(df, aes(x="", y = value, fill=group)) +
  geom_bar(width = 1, stat = "identity") +
  coord_polar("y", start=0)

blank_theme <- theme_minimal()+
  theme(
    axis.title.x = element_blank(),
    axis.title.y = element_blank(),
    axis.text.x=element_blank(),
    panel.border = element_blank(),
    panel.grid=element_blank(),
    axis.ticks = element_blank(),
    plot.title=element_text(size=14, face="bold")
  )

require(scales)
p + scale_fill_brewer("Blues") + blank_theme +
  geom_text(aes(y = value/3 + c(0, cumsum(value)[-length(value)]),
                label = percent(value/100)), size=5)
```

