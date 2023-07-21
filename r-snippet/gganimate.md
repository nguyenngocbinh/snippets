---
title: gganimate
---

```r
library(tidyverse)
library(gganimate)
library(gapminder)
theme_set(theme_classic())

gap <- gapminder %>%
  filter(continent == "Asia") %>%
  group_by(year) %>%
  # The * 1 makes it possible to have non-integer ranks while sliding
  mutate(rank = min_rank(-gdpPercap) * 1) %>%
  ungroup()

p <- ggplot(gap, aes(rank, group = country, 
                     fill = as.factor(country), color = as.factor(country))) +
  geom_tile(aes(y = gdpPercap/2,
                height = gdpPercap,
                width = 0.9), alpha = 0.8, color = NA) +
  
  # text in x-axis (requires clip = "off" in coord_*)
  # paste(country, " ")  is a hack to make pretty spacing, since hjust > 1 
  #   leads to weird artifacts in text spacing.
  geom_text(aes(y = 0, label = paste(country, " ")), vjust = 0.2, hjust = 1) +
  
  coord_flip(clip = "off", expand = FALSE) +
  scale_y_continuous(labels = scales::comma) +
  scale_x_reverse() +
  guides(color = FALSE, fill = FALSE) +
  
  labs(title='{closest_state}', x = "", y = "GFP per capita") +
  theme(plot.title = element_text(hjust = 0, size = 22),
        axis.ticks.y = element_blank(),  # These relate to the axes post-flip
        axis.text.y  = element_blank(),  # These relate to the axes post-flip
        plot.margin = margin(1,1,1,4, "cm")) +
  
  transition_states(year, transition_length = 4, state_length = 1) +
  ease_aes('cubic-in-out')

animate(p, fps = 25, duration = 20, width = 800, height = 600)

```

