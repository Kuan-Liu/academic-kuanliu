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
## 1   1  0.40
## 2   2  2.06
## 3   3  3.50
## 4   4  3.11
## 5   5  5.12
## 6   6  4.82
## 7   7  7.18
## 8   8  7.93
## 9   9  8.31
## 10 10 10.56
```
