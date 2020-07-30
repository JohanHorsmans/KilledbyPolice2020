Webscraping and analysis homicide and police killing data
---------------------------------------------------------

The goal of killedbypolice is to make readily available the data
collected by
<a href="http://killedbypolice.net/" class="uri">http://killedbypolice.net/</a>
for exploration, visualisation, and analysis.

We don’t know much about who collects the data for
<a href="http://killedbypolice.net/" class="uri">http://killedbypolice.net/</a>,
or what their methods are.
[FiveThirtyEight](https://fivethirtyeight.com/features/another-much-higher-count-of-police-homicides/)
reported that he was ‘an instructor on nonviolent physical-intervention
techniques and that he prefers to remain anonymous’.

This is an important data set because the ‘US government has no
comprehensive record of the number of people killed by law enforcement.’
([*The Guardian*, 1 June
2015](https://www.theguardian.com/us-news/ng-interactive/2015/jun/01/about-the-counted)).
The killedbypolice project is one of a few non-government projects that
continuously collect data on police killings (see [Related
work](#related-work) below).

Acknowledgments
---------------

This repo extends Ben Marwick’s work from 2018 in
[KilledbyPolice](https://github.com/benmarwick/killedbypolice) by using
webscraping tools of 2020 and by updating with data with records from
2019 and 2020.

How to use
----------

Start with (1) scrapingdata.Rmd, which teaches you - how to scrape
tables of data from the internet - create charts - create maps (hexbins,
grids) from the data This script takes killedbypolice.net database as
input

Next, you can practice on (2) homicidescraping.Rmd, which has a similar
workflow, but surveys FBI and wikipedia data on homicide incidence per
state in the US for the last decade. This script is unfinished and needs
extra work.

Some explorations
-----------------

Here are some explorations of the data:

The most common age to be killed by police is in the late twenties and
early thirties, and this has not changed much over time.

``` r
library(ggplot2)
library(ggridges)

data %>% 
  filter(Gender %in% c("F", "M", "T")) %>% 
  filter(!is.na(Year)) %>% 
  ggplot(aes(x = Age,
             y = factor(Year),
             fill = Gender)) +
  geom_density_ridges(alpha = 0.5, 
                      scale = 0.9)  +
  theme_ridges(font_size = 10) +
  scale_x_continuous(breaks = seq(0, 100, 10),
                     labels = seq(0, 100, 10)) +
  xlab("Age at death (years)") +
  ylab("Year") +
  theme(axis.title = element_text(size = 14))
```
