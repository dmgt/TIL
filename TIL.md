### Skype a Scientist!
- https://www.skypeascientist.com/ (for teachers and researchers)

### R morsels

#### Quick tips
- Use `vtable` to keep quick list of variables in viewer window without constantly repeating `head(0` or `glipmse()` - demo [here](https://threadreaderapp.com/thread/1060256367909326848.html)
- [Example](https://gist.github.com/cwickham/93c35206b577b350a57d21ed2e5bcef1) of combining `bind_rows()` with `map()` and `read_csv()`
- `knitr::write_bib(c("knitr", "shiny"))` will generate the citation for knitr and shiny
- `glimpse()` or `View()`
- Summary stats beyond `summary()`
    - [skimr](https://github.com/ropensci/skimr) "A frictionless, pipeable approach to dealing with summary statistics"
       - Note the in-line histograms don't render well in knitted files, can turn off (or use `summarytools` below)
    - [summarytools](https://cran.r-project.org/web/packages/summarytools/vignettes/Introduction.html)
       - Use `dfSummary()` for summary stats, valid, missing, and a graph for each variable
- Using `gh` library, can doadload a single file from a public or private GitHub repo (via [Noam Ross](https://twitter.com/noamross/status/1024682912384462848))
- `rvg` and `officer` to make plots editable in MS Excel or Powerpoint ([example](https://twitter.com/noamross/status/1027280341025939457?s=19))
- `gt` for tables


#### Tutorials
- [Experimental Design in R](https://www.datacamp.com/courses/experimental-design-in-r), kaelen medeiros, DataCamp
- [FUNctional programming tricks in httr](https://irene.rbind.io/post/fun-prog-httr/), Irene Steves
- [Beyond Basic R](https://owi.usgs.gov/blog/intro-best-practices/), USGS R

#### Markdown
 
 - [R Markdown: The definitive guide](https://bookdown.org/yihui/rmarkdown/)
 - [Some Lesser Known Features of knitr](https://slides.yihui.name/2018-knitr-RaukR-Yihui-Xie.html#1), Yihui Xie, 2018
 - There is an RStudio add-in called "Infinitive Moon Reader" that [enables](https://slides.yihui.name/2018-knitr-RaukR-Yihui-Xie.html#11) live preview of documents without having to continually knit them 
 - In theory it's possible to use https://yihui.name/tinytex/ instead of MikTeX for future LaTeX installs on Windows, in practice I have yet to do so
 - [Including external source R code](http://zevross.com/blog/2014/07/09/making-use-of-external-r-code-in-knitr-and-r-markdown/), Zev Ross
 - New! - [knitcitations](https://github.com/cboettig/knitcitations) - "Generate citations for knitr markdown and html files"
 - [Thread on thesis organization](https://twitter.com/CivicAngela/status/1024469727274565633), Angela Li
 
#### APIs
- `httr`, and a [tutorial](https://irene.rbind.io/post/fun-prog-httr/) for it by Irene Steves
   - Also [Harnessing the Power of the Web via R Clients for Web APIs](https://www.lucymcgowan.com/talk/asa_joint_statistical_meeting_2018/) , Lucy McGowan, ASA 2018

#### Reproducibility tools in R
- `workflowr`
- `drake`
- ["Happy git with R"](http://happygitwithr.com/)

#### Graphics
 - [Calender graphics with `sugrrants`](https://github.com/earowang/sugrrants/blob/master/README.md)

#### History
- ["R Generation"](https://rss.onlinelibrary.wiley.com/doi/10.1111/j.1740-9713.2018.01169.x), Nick Thieme, Sign Magazine
- ["Teaching R to New Users - From tapply to the Tidyverse"](https://simplystatistics.org/2018/07/12/use-r-keynote-2018/), Roger Peng, UserR! 2018

### Migration guides
- From Excel to R: http://rpubs.com/acolumbus/how-to-use-r-with-excel  (includes list of common Excel functions in R) 
- From MatLab to Python: https://www.enthought.com/white-paper-matlab-to-python/ 

### Python
- [Bicycle control design in python](https://plot.ly/ipython-notebooks/bicycle-control-design/)
- Tests for data in pipelines with [great expectations](https://great-expectations.readthedocs.io/en/latest/intro.html#what-is-great-expectations)

### Version control extras
- [Anonymous GitHub](https://github.com/tdurieux/anonymous_github/) - "a system to anonymize Github repositories before referring to them in a double-blind paper submission"
- [Encrypted git](https://keybase.io/blog/encrypted-git-for-everyone#_)

### General reproducibility
- [OSF + Binder Example of the Future](https://osf.io/wr7an/)
- [Research Compendiums](https://research-compendium.science/)
- ["The practice of reproducible research"](https://www.practicereproducibleresearch.org), including [this](https://www.practicereproducibleresearch.org/case-studies/jmMagallanes.html) case study in R
- ["The importance of reproducible research in high-throughput biology: case studies in forensic bioinformatics"](https://youtu.be/7gYIs7uYbMo), Keith A Baggerly, 2010
- ["Best practices for using google sheets in your data project"](https://matthewlincoln.net/2018/03/26/best-practices-for-using-google-sheets-in-your-data-project.html)
- ["Reproducible research practices, transparency, and open access data in the biomedical literature, 2015–2017"](https://journals.plos.org/plosbiology/article?id=10.1371/journal.pbio.2006930)


#### A few more tools
- Whole Tale
- http://stenci.la/
- OSF

### Data Visualization
 - Online book: [Fundamentals of Data vizualization](https://serialmentor.com/dataviz/) - in R, written using bookdown

### Databases
 - **SQL** stands for Structured Query Language
  - [Star Select SQL](https://selectstarsql.com/) - Free online SQL tutorial 
  - [Tidyverse SQL Translation](https://dbplyr.tidyverse.org/articles/sql-translation.html)
 - **SPARQL** stands for SPARQL Protocol and RDF Query Language
   - ["RDF is a directed, labeled graph data format"](https://www.w3.org/TR/rdf-sparql-query/)
   - SPARQL is canonically pronounced very similarly to `sparklyr`, but they are conceptually very different
   
### Teaching
- [Data Science in a Box](https://rstudio-education.github.io/datascience-box/) - 16-week open source curriculum 
- [Teaching Tech Together](http://teachtogether.tech/en/) - how people learn, how to design and deliver lessons and grow a community of practice
- Preprint: ["Using GitHub classroom to teach statistics"](https://arxiv.org/abs/1811.02021) 

 #### Wikipedia in the classroom
  - Microbiology examples from [Thrash Lab](https://thethrashlab.com/education/)

   
### Stats
 - ["There is still only one test"](http://allendowney.blogspot.com/2016/06/there-is-still-only-one-test.html?m=1), Allen Downey
 - ["Intro Stats and Intro Data Science - do we need both?"](https://speakerdeck.com/minecr/intro-stats-and-intro-data-science-do-we-need-both?),  Mine Cetinkaya-Rundel (RStudio and Associate Professor of the Practice in the Department of Statistical Science at Duke University)   - see teaching examples
 - ["Statistical re-thinking - a Bayeasian course using R and Stan"](https://github.com/rmcelreath/statrethinking_winter2019/blob/master/README.md)
   
### ML   
- [Posters](https://github.com/Avik-Jain/100-Days-Of-ML-Code/blob/master/README.md) by Avik Jain
- h2o.ai, [automl](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/automl.html), and  [automl example with power plant data](https://github.com/h2oai/h2o-tutorials/blob/master/h2o-world-2017/automl/R/automl_regression_powerplant_output.Rmd )
- `caret` will still be supported, [`parsnip`](https://www.tidyverse.org/articles/2018/11/parsnip-0-0-1/) is new and part of the tidyverse
- ["Troubling trends in machine learning scholarship"](http://approximatelycorrect.com/2018/07/10/troubling-trends-in-machine-learning-scholarship/)
- Free online classes:
  - fastai
  - [Bloomberg ML class](https://bloomberg.github.io/foml/#lectures)
  
 ### Grants
  - [Open grants](https://www.ogrants.org/) - includes NSF GRFP examples
  
 

