---
title: R Markdown Page

date: 2020-04-06T00:00:00.000Z
lastmod: 2018-04-09T00:00:00.000Z

draft: false
toc: false
type: docs

linktitle: Heatmaps
menu:
  docs:
    parent: Example Topic
    weight: 2
---

This page provides an example of using R Markdown.

## Code block


```r
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.2     v purrr   0.3.4
## v tibble  3.0.3     v dplyr   1.0.0
## v tidyr   1.1.0     v stringr 1.4.0
## v readr   1.3.1     v forcats 0.5.0
```

```
## -- Conflicts ------------------------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(ggplot2)
library(dplyr)
library(reshape2)
```

```
## 
## Attaching package: 'reshape2'
```

```
## The following object is masked from 'package:tidyr':
## 
##     smiths
```

```r
library(RCurl)
```

```
## 
## Attaching package: 'RCurl'
```

```
## The following object is masked from 'package:tidyr':
## 
##     complete
```

```r
# 1. Read spreadsheet;
x <- getURL("https://raw.githubusercontent.com/ishaberry/Covid19Canada/master/cases.csv")
can_case <- read.csv(text=x, header = TRUE, sep = ",", encoding = 'UTF-8')

can_case$date_report<-strftime(strptime(can_case$date_report,"%d-%m-%Y"),"%m-%d")

on_case <- filter(can_case, province == "Ontario")  %>% group_by(date_report,health_region) %>% summarise(Freq=n())
```

```
## `summarise()` regrouping output by 'date_report' (override with `.groups` argument)
```

```r
qc_case <- filter(can_case, province == "Quebec")  %>% group_by(date_report,health_region) %>% summarise(Freq=n())
```

```
## `summarise()` regrouping output by 'date_report' (override with `.groups` argument)
```

```r
bc_case <- filter(can_case, province == "BC")  %>% group_by(date_report,health_region) %>% summarise(Freq=n())
```

```
## `summarise()` regrouping output by 'date_report' (override with `.groups` argument)
```

```r
ab_case <- filter(can_case, province == "Alberta")  %>% group_by(date_report,health_region) %>% summarise(Freq=n())
```

```
## `summarise()` regrouping output by 'date_report' (override with `.groups` argument)
```

```r
# If you desire to plot after a specific date, for example before I only extract case data reported after March 5th, 2020, 
#you can uncomment and run the code line below;
# on_case <- filter(can_case, province == "Ontario" & date_report > "2020-03-05")  %>% group_by(date_report,health_region) %>% summarise(Freq=n())

# 3. checking the daily case count distribution;
# summary(on_case$Freq)
# Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
# 1.00    1.00    3.00   10.82   12.00  206.00 
#I decide to break daily case numbers in the following groups, 0, 1-9, 10-49, 50-99, >100 (5 levels)

# 4. create daily case groups, relabel in ggplot to 1-9, 10-49, 50-99 and 100+;
on_case <- on_case %>%
  mutate( cases = case_when(
    Freq >=1 & Freq <=9    ~ "1",
    Freq >=10 & Freq <=49  ~ "2",
    Freq >=50 & Freq <=99  ~ "3",
    Freq >=100 & Freq <=499 ~ "4",
    Freq >=500 ~ "5"))

qc_case <- qc_case %>%
  mutate( cases = case_when(
    Freq >=1 & Freq <=9    ~ "1",
    Freq >=10 & Freq <=49  ~ "2",
    Freq >=50 & Freq <=99  ~ "3",
    Freq >=100 & Freq <=499 ~ "4",
    Freq >=500 ~ "5"))

bc_case <- bc_case %>%
  mutate( cases = case_when(
    Freq >=1 & Freq <=9    ~ "1",
    Freq >=10 & Freq <=49  ~ "2",
    Freq >=50 & Freq <=99  ~ "3",
    Freq >=100 & Freq <=499 ~ "4",
    Freq >=500 ~ "5"))

ab_case <- ab_case %>%
  mutate( cases = case_when(
    Freq >=1 & Freq <=9    ~ "1",
    Freq >=10 & Freq <=49  ~ "2",
    Freq >=50 & Freq <=99  ~ "3",
    Freq >=100 & Freq <=499 ~ "4",
    Freq >=500 ~ "5"))

# 5.1 reorder health region by case frequency count, note that toronto should have the highest cumulative frequncy;
on_case_region<- filter(can_case, province == "Ontario" )  %>% group_by(health_region) %>% summarise(Freq=n())
```

```
## `summarise()` ungrouping output (override with `.groups` argument)
```

```r
region_order <- unlist(on_case_region[order(on_case_region$Freq),][,1]) #save new region order by total case frequency to a vector;

# 5.2 update original level to the new ordered regional level;
on_case$health_region<- factor(on_case$health_region, levels=region_order[1:dim(on_case_region)[1]])

# 5.3 update for QC and BC
qc_case_region<- filter(can_case, province == "Quebec" )  %>% group_by(health_region) %>% summarise(Freq=n())
```

```
## `summarise()` ungrouping output (override with `.groups` argument)
```

```r
region_order <- unlist(qc_case_region[order(qc_case_region$Freq),][,1]) #save new region order by total case frequency to a vector;
qc_case$health_region<- factor(qc_case$health_region, levels=region_order[1:dim(qc_case_region)[1]])

bc_case_region<- filter(can_case, province == "BC" )  %>% group_by(health_region) %>% summarise(Freq=n())
```

```
## `summarise()` ungrouping output (override with `.groups` argument)
```

```r
region_order <- unlist(bc_case_region[order(bc_case_region$Freq),][,1]) #save new region order by total case frequency to a vector;
bc_case$health_region<- factor(bc_case$health_region, levels=region_order[1:dim(bc_case_region)[1]])

ab_case_region<- filter(can_case, province == "Alberta" )  %>% group_by(health_region) %>% summarise(Freq=n())
```

```
## `summarise()` ungrouping output (override with `.groups` argument)
```

```r
region_order <- unlist(ab_case_region[order(ab_case_region$Freq),][,1]) #save new region order by total case frequency to a vector;
ab_case$health_region<- factor(ab_case$health_region, levels=region_order[1:dim(ab_case_region)[1]])


# 6.plot;
# png("covid19_oncase_heatmap.png", width = 8, height = 5, units = "in", res = 300)

ggplot(on_case, aes( x=as.factor(reorder(date_report, desc(date_report))),y=health_region)) +
  coord_equal()+
  scale_x_discrete(position = "top")+
  geom_tile(aes(fill = cases )) + 
  geom_text(aes(label = round(Freq, 1)), size=2) +
  scale_fill_brewer(palette = "YlOrRd",label=c("1-9","10-49","50-99","100-499",expression(phantom(x) >=500))) +
  labs(y = " ", x = "",fill="Daily cases",caption = "Daily New COVID-19 Cases by Region in Ontario")+
  theme(panel.background = element_rect(fill = "white", colour = "black"),
        panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(), 
        legend.position = "right",
        legend.key.width=unit(0.25, "cm"),
        legend.key.height =unit(0.25, "cm"),
        legend.text = element_text(size=6),
        legend.title = element_text(size=6),
        axis.title = element_text(size=6),
        axis.text = element_text(size=6),
        axis.text.x = element_text(angle = 90, hjust = 0),
        plot.margin = margin(0,0, 0, 0, "cm"), 
        plot.caption = element_text(hjust=1, size=7)) 
```

<img src="/docs/rmarkdown_files/figure-html/unnamed-chunk-1-1.png" width="672" />

```r
# dev.off()

# png("covid19_bccase_heatmap.png", width = 6.5, height = 3.5, units = "in", res = 300)

ggplot(bc_case, aes( x=as.factor(reorder(date_report, desc(date_report))),y=health_region)) +
  coord_equal()+
  scale_x_discrete(position = "top")+
  geom_tile(aes(fill = cases )) + 
  geom_text(aes(label = round(Freq, 1)), size=2) +
  scale_fill_brewer(palette = "YlOrRd",label=c("1-9","10-49","50-99","100-499",expression(phantom(x) >=500))) +
  labs(y = " ", x = "",fill="Daily cases",caption = "Daily New COVID-19 Cases by Region in British Columbia")+
  theme(panel.background = element_rect(fill = "white", colour = "black"),
        panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(), 
        legend.position = "right",
        legend.key.width=unit(0.25, "cm"),
        legend.key.height =unit(0.25, "cm"),
        legend.text = element_text(size=6),
        legend.title = element_text(size=6),
        axis.title = element_text(size=6),
        axis.text = element_text(size=6),
        axis.text.x = element_text(angle = 90, hjust = 0),
        plot.margin = margin(0,0, 0, 0, "cm"), 
        plot.caption = element_text(hjust=1, size=7)) 
```

<img src="/docs/rmarkdown_files/figure-html/unnamed-chunk-1-2.png" width="672" />

```r
# dev.off()

# png("covid19_qccase_heatmap.png", width = 6.5, height = 3.5, units = "in", res = 300)

ggplot(qc_case, aes( x=as.factor(reorder(date_report, desc(date_report))),y=health_region)) +
  coord_equal()+
  scale_x_discrete(position = "top")+
  geom_tile(aes(fill = cases )) + 
  geom_text(aes(label = round(Freq, 1)), size=2) +
  scale_fill_brewer(palette = "YlOrRd",label=c("1-9","10-49","50-99","100-499",expression(phantom(x) >=500))) +
  labs(y = " ", x = "",fill="Daily cases",caption = "Daily New COVID-19 Cases by Region in Quebec")+
  theme(panel.background = element_rect(fill = "white", colour = "black"),
        panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(), 
        legend.position = "right",
        legend.key.width=unit(0.25, "cm"),
        legend.key.height =unit(0.25, "cm"),
        legend.text = element_text(size=6),
        legend.title = element_text(size=6),
        axis.title = element_text(size=6),
        axis.text = element_text(size=6),
        axis.text.x = element_text(angle = 90, hjust = 0),
        plot.margin = margin(0,0, 0, 0, "cm"), 
        plot.caption = element_text(hjust=1, size=7)) 
```

<img src="/docs/rmarkdown_files/figure-html/unnamed-chunk-1-3.png" width="672" />

```r
# dev.off()


# png("covid19_abcase_heatmap.png", width = 6.5, height = 3.5, units = "in", res = 300)

ggplot(ab_case, aes( x=as.factor(reorder(date_report, desc(date_report))),y=health_region)) +
  coord_equal()+
  scale_x_discrete(position = "top")+
  geom_tile(aes(fill = cases )) + 
  geom_text(aes(label = round(Freq, 1)), size=2) +
  scale_fill_brewer(palette = "YlOrRd",label=c("1-9","10-49","50-99","100-499",expression(phantom(x) >=500))) +
  labs(y = " ", x = "",fill="Daily cases",caption = "Daily New COVID-19 Cases by Region in Alberta")+
  theme(panel.background = element_rect(fill = "white", colour = "black"),
        panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(), 
        legend.position = "right",
        legend.key.width=unit(0.25, "cm"),
        legend.key.height =unit(0.25, "cm"),
        legend.text = element_text(size=6),
        legend.title = element_text(size=6),
        axis.title = element_text(size=6),
        axis.text = element_text(size=6),
        axis.text.x = element_text(angle = 90, hjust = 0),
        plot.margin = margin(0,0, 0, 0, "cm"), 
        plot.caption = element_text(hjust=1, size=7)) 
```

<img src="/docs/rmarkdown_files/figure-html/unnamed-chunk-1-4.png" width="672" />

```r
# dev.off()
```
