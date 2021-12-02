Visualizing the Average Age of Government Representatives
================

## Necessary Packages

``` r
library(ggplot2)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(fivethirtyeight)
library(readr)
```

## Visualization

``` r
avg_congress_age <- congress_age %>%
group_by(termstart, party) %>%
filter(party == "D" | party == "R") %>%
summarize(mean_age = mean(age))
```

    ## `summarise()` has grouped output by 'termstart'. You can override using the `.groups` argument.

``` r
avg_congress_age <- avg_congress_age %>%
mutate(mean_age_months = (mean_age*12))

ggplot(data = avg_congress_age, mapping = aes(x = termstart, y = mean_age , color = party)) +
geom_line() +
coord_cartesian(ylim = c(40, 60)) +
labs(title = "Average Age of Members of Congress",
subtitle = "At start of term, 1947-2013",
x = "Date" , y = "Average age") +
scale_color_manual(values = c("blue", "red"))
```

![](README_files/figure-gfm/pressure-1.png)<!-- -->
