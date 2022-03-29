---
date: "2022-03-29"
draft: false
tags:
- R
- python
- reticulate
- data science
title: Indexing from 0? The Value of R and Python for Data Science
---

## Introduction

These days, a common question among practicing data scientists is, *what is your primary language?*, with "language" often referring either R or Python. This is not a great question, because...

> the reality is R and Python are both incredibly valuable open source computing languagues with different strengths and weaknesses.

The value of each language certainly depends on the task at hand. But ultimately, we suggest these are not only *useful* to the modern data scientist, but are increasingly *expected* to be in the toolbox of the modern data scientist. When applying for data science jobs, interviewees will frequently be asked about and expected to know and use both R and Python.

Yet, there exists a persistent divide between these languages and their users, though this may be thinning a bit with the advent of packages and APIs in both languages that attempt to bridge the divide. For example, the [`reticulate` package](https://rstudio.github.io/reticulate/) in R allows for running Python code in R. Or, though much more narrow in scope by comparison, the [`datar` API](https://pypi.org/project/datar/) in Python allows for usage of tidy functions and packages for data wrangling in Python. 

So, the answers to our opening question (*what is your primary language?*) will vary widely, and are often dependent on the domain of the data scientist. For example, social scientists (e.g., data scientists at survey or market research firms or institutions) or in statistics (e.g., biostats) will often respond with resounding support for R. This can be for many reasons from a nod to the development of R emanating from S and S+ by *statisticians*, with the implication being there are better tools and support for those more routinely practicing *statistical* computing. Or, the norms of the field(s) could be the reasons for preferring R to Python. Further still, R users often point to the simplicity of getting started with R, relative to the perception of a steeper learning curve when getting started with Python. 

On the other hand, if your primary domain is computer science or many of the natural sciences, the answer would be *Python, of course*! This might be also because of norms in the field(s). But often the preference for Python is rooted in it's speed, efficiency, and syntactic elegance. We will come back to this latter point later. Further, Python prefer-ers will also point to the use of Python in so many backends for so many companies, making Python a critical language to support most of what we see and experience in the world on a daily basis, whether we realize it or not.

Though useful to start at the preferential differences between R and Python, in this post, we aren't interested in picking one language over the other. Rather, it's our goal to give a brief overview of some key differences and similarities between Python and R. We will then conclude by offering some thoughts on how they can be used together given their value and position in the modern data science landscape. In our view, usage should primarily be dependent on the task at hand, rather than adherence to norms in the field or a generic bias toward or against one or the other. 

## Indexing from 0?

First, a quick word on the title of this post: *indexing from 0*. This is usually the first, and most often cited point of distinction between Python and R. Though at times this difference might be consequential, typically this difference (at least when it shows up in arguments about Python vs. R) is tangential and largely inconsequential. So, we will side-step taking a position on whether it makes more sense to index from 0 or 1, and instead highlight what this actually means, and use that as a launching point. 

Indexing refers to the position of a value, often in a vector or array. Think of it like counting. If we were to build an object `seq` containing a sequence of values from 1 to 5 in Python, it might look like the following.

```
seq = [1,2,3,4,5]
```

Then, to call this object, we can simply call the object's name in both R and Python, `seq`. 

To call a specific *value* in the sequence, though, we'd use indexing notation (`[ ]`) and refer to the specific position we were interested in. This is the main point of difference between R and Python. For example, to return the first value in the object `seq`, we'd run the following.

```
seq[0]
```

This would return `1`, as the integer 1 occupies the first position in the object `seq`. 

Yet, if we wanted to do the same thing in R, it would look something like this:

```
# first create the object
seq <- c(1,2,3,4,5)

# call the value in the first position
seq[1]
```

This would return a value of 1 as before. But note, we call the position `1`, instead of `0` as we did with the Python snippet above. If we were to call position `0` in R, then we would have returned: `numeric(0)`, meaning 0 is technically a numeric value, but isn't present in the sequence object, `seq`, we created.

This is the simplest way to think about the difference in indexing between R and Python. Again, more complex extensions and examples can certainly be thought of, but this isn't our aim. The point of including this in the title is to give a nod to the distinction between R and Python, which often operates as a colloquial signal of preference more than anything.

## Differences

Let's jump into a look at some key differences between the two languages. First, is simply getting started. 

In R, getting started typically involves two steps: download R, and then download an IDE (integrated development environment) to wrok with R, which is typically RStudio. Whether working from the R console or RStudio, users are officially up and running when they open one of these apps from their desktop. 

In Python, getting started involves downloading Python and an IDE as before. But it can be more confusing as Python is available as a [standalone download](https://www.python.org/downloads/), or as part of a release of [Anaconda](https://www.anaconda.com/). Many people new to Python erroneously think Anaconda is the RStudio IDE equivalent for Python. But Anaconda is *not* an IDE itself, but is rather a platform with a bunch of (mostly) Python related tools and IDEs. For example, within Anaconda, there are several ways to interact with Python such as IPython, Spyder (which is a lot like RStudio), or Jupyter Notebooks. Further still, there are more IDE's beyond the handful included in a typical release of Anaconda that one can use with Python, such as PyCharm. 

Many who use Python use it via an interactive Jupyter Notebook (JN). Though straightforward to use, the quickest way to launch JN is at the command line, which is intimidating to many R users or non-programmers in general. Though the command (assuming directories are organized and a working environment is in place) is simple - `jupyter notebook` - opening a terminal window is intimidating for many, which may turn them off of Python out of the gate.

Next is the issue of environments. Here again, the perception is Python is too complicated. In Python the environment isn't obviously located in the place many users think it is (or even visible on its own). In fact, some users (like myself) prefer to build different environments for different purposes or projects. For example, I built an environment called `pyr`, which includes both an R and Python3 kernel to allow for easy switching between R and Python from within JN. 

On the contrary, if working from RStudio, then the main working environment (the "global environment") is visible in a designated tab in a separate pane whenever RStudio is opened. This environment is populated throughout the session, and all objects, data, functions, etc. are able to be quickly interacted with during the session. The environment can then be saved as a whole, or individual objects or data can be saved from the environment as well (e.g., `save(data_set, file = "data_set.RData")`). Though seemingly small and easily navigable, these differences often push users toward or away from either language. 

Finally, a key difference between R and Python is the syntax. In Python, syntax is typically much cleaner/elegant, compared to R. To steal an example from [Norm Matloff](https://github.com/matloff/R-vs.-Python-for-Data-Science) consider the following `if` statement in Python compared to the same statement in R:

```
# in Python
if x > y: 
   z = 5
   w = 8
   
# in R
if (x > y)
{ 
   z = 5
   w = 8
}
```

There is significantly less clutter as well as cleaner use of indentation in the Python version compared to the R version. 

Also, the assignment operator trips up many who are new to crossing between R and Python. In R, both `=` and `<-` will created objects by assigning values to them. But in Python only `=` is valid for assigning values to objects, while `<-` is meaningless, and throws something like the following error:

```
TypeError: bad operand type for unary -: 'list'
```

## Similarities

Now, let's take a look at a few similarities between R and Python. First and most notably is the common foundation of object oriented programming (OOP). Both R and Python are built on creating objects and manipulating those objects to do stuff. As mentioned previously re: operators, R and Python are the same in that objects are built, manipulated, and interacted to result in different objects, or return outcomes of interest. 

Another related similarity between R and Python is the reliance on functions (which are stored as objects). Functions are the driving force behind operations and engagement with either language. 

> A function is a chunk of code that conducts some operation on the basis of raw values passed to it. 

For example, fitting a model in R relies on the `lm()` function from base R. But in both languages, we can write our own functions, cleverly called, "user defined functions," which allow for custom calculations and operations. So, if we wanted to write our own function to, say, convert temperate from Fahrenheit to Celsius, though the syntax is a bit different, we'd still write a simple function in both languages to make the calculation for us. In short, the intuition is the same, while the syntax is slightly different.

```
# in R
celsius <- function(f) {
  c <- ((f - 32) * 5) / 9
  return(c)
}

# in Python
def celsius(f):
	((f - 32) * 5) / 9
```

Finally, a similarity between R and Python is that they are both open source. This means there is free access to each, and free engagement with the languages, where anyone can contribute code in the form of modules, APIs, or packages. Though these are organized slightly differently in R vs. Python (e.g., Scikit-learn housing many modeling functions in Python, compared to R being typically more reliant on individual packages that are more narrowly focused), the ability to directly contribute code to the language to help a common user base makes R and Python invaluable open source resources that power so much of modern data science. 

## Concluding Remarks & Resources

As alluded to in the introduction, there is not only *room* for both R and Python, but there is a *need* for data scientists and scholars to embrace both R and Python. This is because of the expectations of data scientists in industry these days, as well as the ability to take full advantage of the strengths of each language. As linked earlier, Norm Matloff provides a great comparison of R and Python in the context of data science. Take a look [here](https://github.com/matloff/R-vs.-Python-for-Data-Science). 

Our opinion should be clear at this point: 

> R and Python are both excellent, valuable, open source languages useful for a host of data science and statistical tasks. There shouldn't be "one or the other."

These languages offer immense tools for data scientists and scholars alike, the mastery of which ultimately results in a well-rounded researcher or practitioner. 

To this end, we recommend anyone reading this who is unfamiliar with either to dig into the unfamiliarity and embrace the challenge for both professional gains as well as rounding off a thorough, high quality data science toolbox. To help in this effort, there is an enormous amount of free resources available online, from YouTube videos and tutorials, to blog posts and books. Importantly, as both R and Python are open source, there is a strong push in both communities to keep much of these resources free to all. Here are a few places to get started with each: 

  - R 
    - [Getting Started with R](https://support.rstudio.com/hc/en-us/articles/201141096-Getting-Started-with-R), blog post from RStudio
    - [R for Data Science](https://r4ds.had.co.nz/), free book by Tidyverse architects Hadley Wickham and Garrett Grolemund
    - [Big Book of R](https://www.bigbookofr.com/index.html), list of many R-related books with links and domain-specific resources

  - Python
    - [Python for Beginners](https://www.python.org/about/gettingstarted/), article from Python.org
    - [Getting started with... Python](https://stackoverflow.blog/2021/07/14/getting-started-with-python/), blog post from the Stack Overflow Blog
    - [How to get started with Python programming](https://about.gitlab.com/blog/2021/10/21/beginner-guide-python-programming/), blog post from GitLab

Finally, we have mentioned a lot of technology in this post. Here are some helpful links for some core R and Python software and tools: 

  - [R](https://www.r-project.org/)
  - [RStudio](https://www.rstudio.com/products/rstudio/download/)
  - [Python](https://www.python.org/)
  - [Anaconda](https://www.anaconda.com/)
  - [PyCharm](https://www.jetbrains.com/pycharm/)
  - [Jupyter Notebooks](https://jupyter.org/)
  - [Scikit-Learn](https://scikit-learn.org/stable/)
  - [Tidyverse](https://www.tidyverse.org/)
  - Matloff's discussion of [R vs. Python for Data Science](https://github.com/matloff/R-vs.-Python-for-Data-Science)
