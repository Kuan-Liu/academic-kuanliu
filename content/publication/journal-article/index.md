---
title: "Estimation of causal effects with repeatedly measured outcomes in a Bayesian framework"
authors:
- admin
- Olli Saarela
- Brian M. Feldman
- Eleanor Pullenayegum
date: "2020-01-29T00:00:00Z"
doi: "https://doi.org/10.1177/0962280219900362"

# Schedule page publish date (NOT publication's date).
# publishDate: "2017-01-01T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["2"]

# Publication name and optional abbreviated publication name.
publication: "*Statistical Methods in Medical Research*"
publication_short: ""

# abstract: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum. Sed ac faucibus dolor, scelerisque sollicitudin nisi. Cras purus urna, suscipit quis sapien eu, pulvinar tempor diam. Quisque risus orci, mollis id ante sit amet, gravida egestas nisl. Sed ac tempus magna. Proin in dui enim. Donec condimentum, sem id dapibus fringilla, tellus enim condimentum arcu, nec volutpat est felis vel metus. Vestibulum sit amet erat at nulla eleifend gravida.

# Summary. An optional shortened abstract.
# summary: Lorem ipsum dolor sit amet, consectetur adipiscing elit. Duis posuere tellus ac convallis placerat. Proin tincidunt magna sed ex sollicitudin condimentum.

tags:
- Featured articles
featured: true

# links:
# - name: ""
#   url: ""
# url_pdf: http://arxiv.org/pdf/1512.04133v1
# url_code: ''
# url_dataset: ''
# url_poster: ''
# url_project: ''
# url_slides: ''
# url_source: ''
# url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/jdD8gXaTZsc)'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
# projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
# slides: example

---

**Abstract**

Constructing causal inference methods to handle longitudinal data in observational studies is of high interest. In an observational setting, treatment assignment at each clinical visit follows a decision strategy where the treating clinician selects treatment based on current and past clinical measurements as well as treatment histories. These time-dependent structures, coupled with inherent correlations between and within each visit, add on to the data complexity. Despite recent interest in Bayesian causal methods, only a limited literature has explored approaches to handle longitudinal data and no method handles repeatedly measured outcomes. In this paper, we extended two Bayesian approaches: Bayesian estimation of marginal structural models and two-stage Bayesian propensity score analysis to handle a repeatedly measured outcome. Our proposed methods permit causal estimation of treatment effects at each visit. Time-dependent inverse probability of treatment weights are obtained from the Markov chain Monte Carlo samples of the posterior treatment assignment model for each follow-up visit. We use a simulation study to validate and compare the proposed methods and illustrate our approaches through a study of intravenous immunoglobulin therapy in treating newly diagnosed juvenile dermatomyositis.
