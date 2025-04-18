--- 
title: "Supervised Machine Learning for Text Analysis in R"
author: "Emil Hvitfeldt and Julia Silge"
date: "2022-05-11"
site: bookdown::bookdown_site
documentclass: krantz
bibliography: [book.bib]
link-citations: yes
links-as-notes: true
colorlinks: true
lot: false
lof: false
monofont: "Source Code Pro"
monofontoptions: "Scale=0.7"
github-repo: EmilHvitfeldt/smltar
description: "Supervised Machine Learning for Text Analysis in R"
cover-image: cover.jpg
url: https://smltar.com
graphics: yes
---



\mainmatter


# Welcome to Supervised Machine Learning for Text Analysis in R {-}

This is the [website](https://smltar.com/) for *Supervised Machine Learning for Text Analysis in R*! Visit the [GitHub repository for this site](https://github.com/EmilHvitfeldt/smltar), or buy a physical copy from [CRC Press](https://doi.org/10.1201/9781003093459), [Bookshop.org](https://bookshop.org/books/supervised-machine-learning-for-text-analysis-in-r-9780367554194/9780367554194), or [Amazon](https://amzn.to/3DaHzjF). 

<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br />This online work by [Emil Hvitfeldt](https://www.emilhvitfeldt.com/) and [Julia Silge](http://juliasilge.com/) is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.


\pagenumbering{roman}
\setcounter{page}{11}

# Preface {-}

Modeling as a statistical practice can encompass a wide variety of activities. This book focuses on *supervised or predictive modeling for text*, using text data to make predictions about the world around us. We use the [tidymodels](https://www.tidymodels.org/) framework for modeling, a consistent and flexible collection of R packages developed to encourage good statistical practice.

Supervised machine learning using text data involves building a statistical model to estimate some output from input that includes language. The two types of models we train in this book are regression and classification. Think of \index{regression}regression models as predicting numeric or continuous outputs, such as predicting the year of a United States Supreme Court opinion from the text of that opinion. Think of \index{classification}classification models as predicting outputs that are discrete quantities or class labels, such as predicting whether a GitHub issue is about documentation or not from the text of the issue. Models like these can be used to make predictions for new observations, to understand what features or characteristics contribute to differences in the output, and more. We can evaluate our models using performance metrics to determine which are best, which are acceptable for our specific context, and even which are fair.

<div class="rmdnote">
<p>Text data is important for many domains, from healthcare to marketing to the digital humanities, but specialized approaches are necessary to create features (predictors) for machine learning from language.</p>
</div>

Natural language that we as speakers and/or writers use must be dramatically transformed to a machine-readable, numeric representation to be ready for computation. In this book, we explore typical text preprocessing steps from the ground up and consider the effects of these steps. We also show how to fluently use the **textrecipes** R package [@textrecipes] to prepare text data within a modeling pipeline.

@Silge2017 provides a practical introduction to text mining with R using tidy data principles, based on the **tidytext** package. If you have already started on the path of gaining insight from your text data, a next step is using that text directly in predictive modeling. Text data contains within it latent information that can be used for insight, understanding, and better decision-making, and predictive modeling with text can bring that information and insight to light. If you have already explored how to analyze text as demonstrated in @Silge2017, this book will move one step further to show you how to *learn and make predictions* from that text data with supervised models. If you are unfamiliar with this previous work, this book will still provide a robust introduction to how text can be represented in useful ways for modeling and a diverse set of supervised modeling approaches for text.


## Outline {-}

The book is divided into three sections. We make a (perhaps arbitrary) distinction between *machine learning methods* and *deep learning methods* by defining deep learning as any kind of multilayer neural network (LSTM, bi-LSTM, CNN) and machine learning as anything else (regularized regression, naive Bayes, SVM, random forest). We make this distinction both because these different methods use separate software packages and modeling infrastructure, and from a pragmatic point of view, it is helpful to split up the chapters this way. 

- **Natural language features:** How do we transform text data into a representation useful for modeling? In these chapters, we explore the most common preprocessing steps for text, when they are helpful, and when they are not.

- **Machine learning methods:** We investigate the power of some of the simpler and more lightweight models in our toolbox.

- **Deep learning methods:** Given more time and resources, we see what is possible once we turn to neural networks. 

Some of the topics in the second and third sections overlap as they provide different approaches to the same tasks.

Throughout the book, we will demonstrate with examples and build models using a selection of text data sets. A description of these data sets can be found in Appendix \@ref(appendixdata).

<div class="rmdnote">
<p>We use three kinds of info boxes throughout the book to invite attention to notes and other ideas.</p>
</div>

<div class="rmdwarning">
<p>Some boxes call out warnings or possible problems to watch out for.</p>
</div>

<div class="rmdpackage">
<p>Boxes marked with hexagons highlight information about specific R packages and how they are used. We use <strong>bold</strong> for the names of R packages.</p>
</div>


## Topics this book will not cover {-}

This book serves as a thorough introduction to prediction and modeling with text, along with detailed practical examples, but there are many areas of natural language processing we do not cover. \index{CRAN}The [*CRAN Task View on Natural Language Processing*](https://cran.r-project.org/web/views/NaturalLanguageProcessing.html) provides details on other ways to use R for computational linguistics. Specific topics we do not cover include:

- **Reading text data into memory:** Text data may come to a data practitioner in any of a long list of heterogeneous formats. Text data exists in PDFs, databases, plain text files (single or multiple for a given project), websites, APIs, literal paper, and more. The skills needed to access and sometimes wrangle text data sets so that they are in memory and ready for analysis are so varied and extensive that we cannot hope to cover them in this book. We point readers to R packages such as **readr** [@R-readr], **pdftools** [@R-pdftools], and **httr** [@R-httr], which we have found helpful in these tasks.

- **Unsupervised machine learning for text:** @Silge2017 provide an introduction to one method of unsupervised text modeling\index{machine learning!unsupervised}, and Chapter \@ref(embeddings) does dive deep into word embeddings, which learn from the latent structure in text data. However, many more unsupervised machine learning algorithms can be used for the goal of learning about the structure or distribution of text data when there are no outcome or output variables to predict.

- **Text generation:** The deep learning model architectures we discuss in Chapters \@ref(dldnn), \@ref(dllstm), and \@ref(dlcnn) can be used to generate new text\index{text generation}, as well as to model existing text. @Chollet2018 provide details on how to use neural network architectures and training data for text generation.

- **Speech processing:** Models that detect words in audio recordings of speech\index{speech} are typically based on many of the principles outlined in this book, but the training data is _audio_ rather than written text. R users can access pre-trained speech-to-text models via large cloud providers, such as Google Cloud's Speech-to-Text API accessible in R through the **googleLanguageR** package [@R-googleLanguageR].

- **Machine translation:** Machine translation\index{translation} of text between languages, based on either older statistical methods or newer neural network methods, is a complex, involved topic. Today, the most successful and well-known implementations of machine translation are proprietary, because large tech companies have access to both the right expertise and enough data in multiple languages to train successful models for general machine translation. Google is one such example, and Google Cloud's Translation API is again available in R through the **googleLanguageR** package.

## Who is this book for? {-}

This book is designed to provide practical guidance and directly applicable knowledge for data scientists and analysts who want to integrate text into their modeling pipelines. 

We assume that the reader is somewhat familiar with R, predictive modeling concepts for non-text data, and the [**tidyverse**](https://www.tidyverse.org/) family of packages [@Wickham2019]. For users who don't have this background with tidyverse code, we recommend [*R for Data Science*](http://r4ds.had.co.nz/) [@Wickham2017]. Helpful resources for getting started with modeling and machine learning include a [free interactive course](https://supervised-ml-course.netlify.app/) developed by one of the authors (JS) and [*Hands-On Machine Learning with R*](https://bradleyboehmke.github.io/HOML/) [@Boehmke2019], as well as [*An Introduction to Statistical Learning*](http://faculty.marshall.usc.edu/gareth-james/ISL/) [@James2013].  

We don't assume an extensive background in text analysis, but [*Text Mining with R*](https://www.tidytextmining.com/) [@Silge2017], by one of the authors (JS) and David Robinson, provides helpful skills in exploratory data analysis for text that will promote successful text modeling. This book is more advanced than *Text Mining with R* and will help practitioners use their text data in ways not covered in that book.

## Acknowledgments {-}

We are so thankful for the contributions, help, and perspectives of people who have supported us in this project. There are several we would like to thank in particular.

We would like to thank Max Kuhn and Davis Vaughan for their investment in the **tidymodels** packages, David Robinson for his collaboration on the **tidytext** package, and Yihui Xie for his work on **knitr**, **bookdown**, and the R Markdown ecosystem. Thank you to Desirée De Leon for the site design of the online work and to Sarah Lin for the expert creation of the published work's index. We would also like to thank Carol Haney, Kasia Kulma, David Mimno, Kanishka Misra, and an additional anonymous technical reviewer for their detailed, insightful feedback that substantively improved this book, as well as our editor John Kimmel for his perspective and guidance during the process of writing and publishing.



This book was written in the open, and multiple people contributed via pull requests or issues. Special thanks goes to the four people who contributed via GitHub pull requests (in alphabetical order by username): \@fellennert, Riva Quiroga (\@rivaquiroga), Darrin Speegle (\@speegled), Tanner Stauss (\@tmstauss).

Note box icons by Smashicons from flaticon.com.

## Colophon {-}

This book was written in [RStudio](https://www.rstudio.com/ide/) using [**bookdown**](https://bookdown.org). The [website](https://smltar.com) is hosted via [GitHub Pages](https://pages.github.com), and the complete source is available on [GitHub](https://github.com/EmilHvitfeldt/smltar). We generated all plots in this book using [**ggplot2**](https://ggplot2.tidyverse.org) and its light theme (`theme_light()`). The `autoplot()` method for [`conf_mat()`](https://yardstick.tidymodels.org/reference/conf_mat.html) has been modified slightly to allow colors; modified code can be found [online](https://github.com/EmilHvitfeldt/smltar/blob/master/_common.R).

<div class="rmdwarning">
<p>Because of changes in package versions since the publication of the first edition, you may notice slight differences in some results when comparing this online work and the published paper edition.</p>
</div>

This version of the book was built with R version 4.2.0 (2022-04-22) and the following packages:


|package        |version |source                        |
|:--------------|:-------|:-----------------------------|
|bench          |1.1.2   |CRAN (R 4.2.0)                |
|bookdown       |0.26    |CRAN (R 4.2.0)                |
|broom          |0.8.0   |CRAN (R 4.2.0)                |
|corpus         |0.10.2  |CRAN (R 4.2.0)                |
|dials          |0.1.1   |CRAN (R 4.2.0)                |
|discrim        |0.2.0   |CRAN (R 4.2.0)                |
|doParallel     |1.0.17  |CRAN (R 4.2.0)                |
|glmnet         |4.1-4   |CRAN (R 4.2.0)                |
|gt             |0.5.0   |CRAN (R 4.2.0)                |
|hcandersenr    |0.2.0   |CRAN (R 4.2.0)                |
|htmltools      |0.5.2   |CRAN (R 4.2.0)                |
|htmlwidgets    |1.5.4   |CRAN (R 4.2.0)                |
|hunspell       |3.0.1   |CRAN (R 4.2.0)                |
|irlba          |2.3.5   |CRAN (R 4.2.0)                |
|jiebaR         |0.11    |CRAN (R 4.2.0)                |
|jsonlite       |1.8.0   |CRAN (R 4.2.0)                |
|kableExtra     |1.3.4   |CRAN (R 4.2.0)                |
|keras          |2.8.0   |CRAN (R 4.2.0)                |
|klaR           |1.7-0   |CRAN (R 4.2.0)                |
|LiblineaR      |2.10-12 |CRAN (R 4.2.0)                |
|lime           |0.5.2   |CRAN (R 4.2.0)                |
|lobstr         |1.1.1   |CRAN (R 4.2.0)                |
|naivebayes     |0.9.7   |CRAN (R 4.2.0)                |
|parsnip        |0.2.1   |CRAN (R 4.2.0)                |
|prismatic      |1.1.0   |CRAN (R 4.2.0)                |
|quanteda       |3.2.1   |CRAN (R 4.2.0)                |
|ranger         |0.13.1  |CRAN (R 4.2.0)                |
|recipes        |0.2.0   |CRAN (R 4.2.0)                |
|remotes        |2.4.2   |CRAN (R 4.2.0)                |
|reticulate     |1.24    |CRAN (R 4.2.0)                |
|rsample        |0.1.1   |CRAN (R 4.2.0)                |
|rsparse        |0.5.0   |CRAN (R 4.2.0)                |
|scico          |1.3.0   |CRAN (R 4.2.0)                |
|scotus         |1.0.0   |Github (EmilHvitfeldt/scotus) |
|servr          |0.24    |CRAN (R 4.2.0)                |
|sessioninfo    |1.2.2   |CRAN (R 4.2.0)                |
|slider         |0.2.2   |CRAN (R 4.2.0)                |
|SnowballC      |0.7.0   |CRAN (R 4.2.0)                |
|spacyr         |1.2.1   |CRAN (R 4.2.0)                |
|stopwords      |2.3     |CRAN (R 4.2.0)                |
|styler         |1.7.0   |CRAN (R 4.2.0)                |
|text2vec       |0.6.1   |CRAN (R 4.2.0)                |
|textdata       |0.4.2   |CRAN (R 4.2.0)                |
|textfeatures   |0.3.3   |CRAN (R 4.2.0)                |
|textrecipes    |0.5.2   |CRAN (R 4.2.0)                |
|tfruns         |1.5.0   |CRAN (R 4.2.0)                |
|themis         |0.2.1   |CRAN (R 4.2.0)                |
|tidymodels     |0.2.0   |CRAN (R 4.2.0)                |
|tidytext       |0.3.2   |CRAN (R 4.2.0)                |
|tidyverse      |1.3.1   |CRAN (R 4.2.0)                |
|tokenizers     |0.2.1   |CRAN (R 4.2.0)                |
|tokenizers.bpe |0.1.0   |CRAN (R 4.2.0)                |
|tufte          |0.12    |CRAN (R 4.2.0)                |
|tune           |0.2.0   |CRAN (R 4.2.0)                |
|UpSetR         |1.4.0   |CRAN (R 4.2.0)                |
|vip            |0.3.2   |CRAN (R 4.2.0)                |
|widyr          |0.1.4   |CRAN (R 4.2.0)                |
|workflows      |0.2.6   |CRAN (R 4.2.0)                |
|yardstick      |0.0.9   |CRAN (R 4.2.0)                |
