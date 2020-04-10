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
## 1   1  0.89
## 2   2  2.16
## 3   3  3.24
## 4   4  2.64
## 5   5  4.37
## 6   6  5.06
## 7   7  7.89
## 8   8  6.01
## 9   9  9.88
## 10 10 10.79
```
