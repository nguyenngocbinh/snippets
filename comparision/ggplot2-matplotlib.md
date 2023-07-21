---
title: `ggplot2` vs. `matplotlib`
---

Below is a markdown table comparing the features of `ggplot2` (R) and `matplotlib` (Python) for creating visualizations:

1. Plot basics

    | ggplot2 (R)                   |      Feature                                   | matplotlib (Python)                                |
    |---------------------------|---------------------------------------------------|----------------------------------------------------|
    | aes()                 | Used inside `ggplot()` to map variables to aesthetics | Not used; column names are specified directly in `plot()` |
    | +(<gg>) %>%           | Used to add layers and modify the plot            | Not applicable                                     |
    | ggsave()              | Save the plot to a file                           | Not applicable; plots are saved using `plt.savefig()` in Matplotlib |
    | quickplot()           | Simple, intuitive function for quick plots        | Not available                                      |

2. Layers

    | ggplot2 (R)           |      Feature                                      | matplotlib (Python)                               |
    |-----------------------|---------------------------------------------------|---------------------------------------------------|
    | geom_abline()         | Add an arbitrary line to the plot                 | `axhline()` and `axvline()` in Matplotlib         |
    | geom_hline()          | Add horizontal lines to the plot                  | `axhline()` in Matplotlib                         |
    | geom_vline()          | Add vertical lines to the plot                    | `axvline()` in Matplotlib                         |
    | geom_bar()            | Create bar charts                                 | `kind='bar'` in `plot()`                          |
    | geom_col()            | Create column charts                              | `kind='bar'` with `position='identity'` in `plot()`|
    | stat_count()          | Create bar charts with automatic counting         | `kind='bar'` with `position='identity'` in `plot()`|
    | geom_boxplot()        | Create boxplots                                   | `kind='box'` in `plot()`                          |
    | stat_boxplot()        | Create boxplots with statistical summaries        | `kind='box'` in `plot()`                          |
    | geom_map()            | Plot spatial data on maps                         | Not available                                      |
    | geom_point()          | Create scatter plots                              | `kind='scatter'` in `plot()`                      |
    | geom_label()          | Add text labels to points                         | Not available                                      |
    | geom_text()           | Add text annotations to the plot                  | `text()` in Matplotlib                            |
    | geom_violin()         | Create violin plots                               | Not available                                      |
    | stat_ydensity()       | Compute density for violin plots                  | Not available                                      |

3. Position adjustment    
    
    | ggplot2 (R)           |      Feature                                      | matplotlib (Python)                               |
    |-----------------------|---------------------------------------------------|---------------------------------------------------|
    | position_dodge()      | Dodge overlapping elements                        | Not available                                      |
    
4. Annotations

    | ggplot2 (R)           |      Feature                                      | matplotlib (Python)                               |
    |-----------------------|---------------------------------------------------|---------------------------------------------------|
    | annotate()            | Add annotations to the plot                       | Not available                                     |

5. Scales

    | ggplot2 (R)           |      Feature                                      | matplotlib (Python)                               |
    |-----------------------|---------------------------------------------------|---------------------------------------------------|
    | labs()                | Modify plot labels and titles                     | Not available                                     |
    | xlab()                | Modify the x-axis label                           | `set_xlabel()` in Matplotlib                      |
    | ylab()                | Modify the y-axis label                           | `set_ylabel()` in Matplotlib                      |
    | ggtitle()             | Add a plot title                                  | `set_title()` in Matplotlib                       |
    | lims()                | Set plot limits                                   | `set_xlim()` and `set_ylim()` in Matplotlib       |
    | xlim()                | Set x-axis limits                                 | `set_xlim()` in Matplotlib                        |
    | ylim()                | Set y-axis limits                                 | `set_ylim()` in Matplotlib                        |
    | scale_x_continuous()  | Modify x-axis scales                              | `set_xscale()` in Matplotlib                      |
    | scale_y_continuous()  | Modify y-axis scales                              | `set_yscale()` in Matplotlib                      |
    | scale_x_date()        | Modify x-axis scales for date data                | Not available                                      |
    | scale_y_date()        | Modify y-axis scales for date data                | Not available                                      |
    | scale_x_discrete()    | Modify x-axis scales for discrete data            | Not available                                      |
    | scale_y_discrete()    | Modify y-axis scales for discrete data            | Not available                                      |

6. Facetting

    | ggplot2 (R)           |      Feature                                      | matplotlib (Python)                               |
    |-----------------------|---------------------------------------------------|---------------------------------------------------|  
    | facet_wrap()          | Create small multiples in a wrap layout           | `subplots=True` with multiple plots in Pandas     |
    | facet_grid()          | Create small multiples in a grid layout           | `subplots=True` with multiple plots in Pandas     |
    | coord_flip()          | Flip the x and y-axis                            | Not available                                      |

7. Themes

    | ggplot2 (R)           |      Feature                                      | matplotlib (Python)                               |
    |-----------------------|---------------------------------------------------|---------------------------------------------------|  
    | element_blank()       | Remove an element from the plot                   | Not available                                      |
    | element_rect()        | Modify rectangle elements in the plot             | Not available                                      |
    | element_line()        | Modify line elements in the plot                  | Not available                                      |
    | element_text()        | Modify text elements in the plot                  | Not available                                      |

8. autoplot

    | ggplot2 (R)           |      Feature                                      | matplotlib (Python)                               |
    |-----------------------|---------------------------------------------------|---------------------------------------------------|  
    | autoplot()            | Create basic plots automatically                 | Not available                                      |

Please note that `ggplot2` and `matplotlib` are both powerful visualization libraries, but they have different philosophies and strengths. The syntax for creating visualizations can differ significantly between the two libraries.