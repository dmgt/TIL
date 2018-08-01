### R morsels

#### Quick tips
- `spelling::spell_check_setup()` to check for spelling errors or missing quotes (via [Carl Boettiger on Twitter](https://twitter.com/cboettig/status/1017257307263066112?s=19))
- `knitr::write_bib(c("knitr", "shiny"))` will generate the citation for knitr and shiny
- `glimpse()` or `View()`
- [skimr](https://github.com/ropensci/skimr) "A frictionless, pipeable approach to dealing with summary statistics"


#### Tutorials
- [Experimental Design in R](https://www.datacamp.com/courses/experimental-design-in-r), kaelen medeiros, DataCamp
- [FUNctional programming tricks in httr](https://irene.rbind.io/post/fun-prog-httr/), Irene Steves

#### Markdown
 
 - [R Markdown: The definitive guide](https://bookdown.org/yihui/rmarkdown/)
 - [Some Lesser Known Features of knitr](https://slides.yihui.name/2018-knitr-RaukR-Yihui-Xie.html#1), Yihui Xie, 2018
 - There is an RStudio add-in called "Infinitive Moon Reader" that [enables](https://slides.yihui.name/2018-knitr-RaukR-Yihui-Xie.html#11) live preview of documents without having to continually knit them 
 - In theory it's possible to use https://yihui.name/tinytex/ instead of MikTeX for future LaTeX installs on Windows, in practice I have yet to do so
 - [Including external source R code](http://zevross.com/blog/2014/07/09/making-use-of-external-r-code-in-knitr-and-r-markdown/), Zev Ross
 
#### APIs
- `httr`, and a [tutorial](https://irene.rbind.io/post/fun-prog-httr/) for it by Irene Steves

#### Reproducibility tools in R
- `workflowr`
- `drake`

#### Graphics
 - [Calender graphics with `sugrrants`](https://github.com/earowang/sugrrants/blob/master/README.md)

#### History
- ["R Generation"](https://rss.onlinelibrary.wiley.com/doi/10.1111/j.1740-9713.2018.01169.x), Nick Thieme, Sign Magazine
- ["Teaching R to New Users - From tapply to the Tidyverse"](https://simplystatistics.org/2018/07/12/use-r-keynote-2018/), Roger Peng, UserR! 2018

### General reproducibility
- ["The practice of reproducible research"](https://www.practicereproducibleresearch.org), including [this](https://www.practicereproducibleresearch.org/case-studies/jmMagallanes.html) case study in R
- ["The importance of reproducible research in high-throughput biology: case studies in forensic bioinformatics"](https://youtu.be/7gYIs7uYbMo), Keith A Baggerly, 2010

#### A few more tools
- Whole Tale
- http://stenci.la/
- OSF


### Databases
 - **SQL** stands for Structured Query Language
 - **SPARQL** stands for SPARQL Protocol and RDF Query Language
   - ["RDF is a directed, labeled graph data format"](https://www.w3.org/TR/rdf-sparql-query/)
   - SPARQL is canonically pronounced very similarly to `sparklyr`, but they are conceptually very different
   
### Stats
 - ["There is still only one test"](http://allendowney.blogspot.com/2016/06/there-is-still-only-one-test.html?m=1), Allen Downey
   
### ML   
- [Posters](https://github.com/Avik-Jain/100-Days-Of-ML-Code/blob/master/README.md) by Avik Jain
- h2o.ai, [automl](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/automl.html), and  [automl example with power plant data](https://github.com/h2oai/h2o-tutorials/blob/master/h2o-world-2017/automl/R/automl_regression_powerplant_output.Rmd )
- ["Troubling trends in machine learning scholarship"](http://approximatelycorrect.com/2018/07/10/troubling-trends-in-machine-learning-scholarship/)
- Free online classes:
  - fastai
  - [Bloomberg ML class](https://bloomberg.github.io/foml/#lectures)

