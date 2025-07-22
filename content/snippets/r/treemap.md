---
title: tree map
---

```r
library(ggplot2)
library(treemapify)

if(!require(treemapify)) install.packages("treemapify")

data(G20)

ggplot(G20, aes(area = gdp_mil_usd, fill = hdi)) +
  geom_treemap()

ggplot(G20, aes(area = gdp_mil_usd, fill = hdi, label = country)) +
  geom_treemap() +
  geom_treemap_text(fontface = "italic", colour = "white", place = "centre",
                    grow = TRUE)


ggplot(G20, aes(area = gdp_mil_usd, fill = hdi, label = country,
                subgroup = region)) +
  geom_treemap() +
  geom_treemap_subgroup_border() +
  geom_treemap_subgroup_text(place = "centre", grow = T, alpha = 0.5, colour =
                               "black", fontface = "italic", min.size = 0) +
  geom_treemap_text(colour = "white", place = "topleft", reflow = T)

ggplot(G20, aes(area = gdp_mil_usd, fill = region, label = country, subgroup = region)) +
  geom_treemap() +
  geom_treemap_text(grow = T, reflow = T, colour = "black") +
  facet_wrap( ~ hemisphere) +
  scale_fill_brewer(palette = "Set1") +
  theme(legend.position = "bottom") +
  labs(
    title = "The G-20 major economies by hemisphere",
    caption = "The area of each tile represents the country's GDP as a
    proportion of all countries in that hemisphere",
    fill = "Region"
  )

```
