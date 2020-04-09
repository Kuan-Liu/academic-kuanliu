---
title: Survival Analysis I - Cox model diagnostics
event: Guest lecture talk
# event_url: https://example.org

location: Toronto, ON
# address:
#   street: 
#   city: Toronto
#   region: ON
#   postcode: 
#   country: Canada

summary: Guest lecture talk on Cox proportional hazard model diagnostics.

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: "2020-02-26T14:00:00Z"
date_end: "2030-02-26T15:30:00Z"
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: "2017-01-01T00:00:00Z"

authors: []
tags: []

# Is this a featured talk? (true/false)
featured: true

image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/bzdhc5b3Bxs)'
  focal_point: Right

links:
# - icon: twitter
#   icon_pack: fab
#   name: Follow
#   url: https://twitter.com/georgecushen
url_code: ""
url_pdf: "files/survivalslides.pdf"
url_slides: "files/survivalslides.pdf"
url_video: ""

# Markdown Slides (optional).
#   Associate this talk with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
# slides: example

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects:
# - internal-project

# Enable math on this page?
math: true
---

**Lecture Overview**

1. Breslow estimator
    * Learn how to derive and compute Breslow estimator for cumulative baseline hazard
2. COX model diagnostics
    * Martinagle and Deviance residuals are use to assess linearity
    * Score residuals and dfbeta measures are used to identify influential observations;
    * Schoenfeld residuals are used to assess PH assumption
    * Testing significance of the correlation between Schoenfeld residuals and time;
3. Modelling time-dependent covariates in COX model
    * Assessing the significance of the interaction term between covariates and time




