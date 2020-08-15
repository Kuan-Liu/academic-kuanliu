---
title: R Markdown Page

date: 2018-09-09T00:00:00.000Z
lastmod: 2018-09-09T00:00:00.000Z

draft: false
toc: true
type: docs

linktitle: R Markdown Example
menu:
  docs:
    parent: Example Topic
    weight: 2
---

This page provides an example of using R Markdown.

## Code block


```r
x <- 1:10
y <- round(rnorm(10, x, 1), 2)
df <- data.frame(x, y)
df
```

```
##     x     y
## 1   1  1.81
## 2   2  3.69
## 3   3  3.15
## 4   4  3.62
## 5   5  4.90
## 6   6  7.60
## 7   7  5.47
## 8   8  8.06
## 9   9  8.43
## 10 10 10.03
```
