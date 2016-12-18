---
layout:     post
title:      Which is better for data analysis: R or Python? (From Quora)
category:   [Data Mining] 
tags:		[Data Mining, R, Python]
---

This article is from [Quora](https://www.quora.com/Which-is-better-for-data-analysis-R-or-Python)

The answer is from [Vik Paruchuri](https://www.quora.com/profile/Vik-Paruchuri)

Python has come up a long way in data analysis with its Scipy, Numpy and Pandas platforms. Is R still a better data analysis language than Python? Has anyone else used Python with Pandas to a large extent in data analysis projects?

For most data analysis projects, your goal is going to be to create the highest quality analysis in the least amount of time.

If you understand the underlying concepts behind what you’re doing, then you can use either language to perform your analysis.

For example, if you understand the principles of natural language processing, data cleaning, and machine learning, you can implement an automated text summarizer in R or Python.

As this blog post shows, the code in R and Python isn’t even that different for most tasks. At Dataquest, we teach data analysis and data science using Python because it’s better for beginners, but we focus on teaching concepts for this reason.

As time goes on, data analysis in R and Python is becoming more similar as great packages like pandas, rvest, and ggplot bring concepts from one language into the other.

Given that, for most cases, I would use whatever language you’re most familiar with. Here are some main points of differentiation between the languages to be aware of, though:

R has a much bigger library of statistical packages

If you’re doing specialized statistical work, R packages cover more techniques. You can find R packages for a wide variety of statistical tasks using the CRAN task view. R packages cover everything from Psychometrics to Genetics to Finance. Although Python, through SciPy and packages like statsmodels, covers the most common techniques, R is far ahead.

Python is better for building analytics tools

R and Python are equally good if you want to find outliers in a dataset, but if you want to create a web service to enable other people to upload datasets and find outliers, Python is better. Python is a general purpose programming language, which means that people have built modules to create websites, interact with a variety of databases, and manage users.

In general, if you want to build a tool or service that uses data analysis, Python is a better choice.

R builds in data analysis functionality by default, whereas Python relies on packages

Because Python is a general purpose language, most data analysis functionality is available through packages like NumPy and pandas. However, R was built with statistics and data analysis in mind, so many tools that have been added to Python through packages are built into base R.

Python is better for deep learning

Through packages like Lasagne, caffe, keras, and tensorflow, creating deep neural networks is straightforward in Python. Although some of these, like tensorflow, are being ported to R, support is still far better in Python.

Python relies on a few main packages, whereas R has hundreds

In Python, sklearn is the “primary” machine learning package, and pandas is the “primary” data analysis package. This makes it easy to know how to accomplish a task, but also means that a lot of specialized techniques aren’t possible.

R, on the other hand, has hundreds of packages and ways to accomplish things. Although there’s generally an accepted way to accomplish things, the lines between base R, packages, and the tidyverse can be fuzzy for inexperienced folks.

R is better for data visualization

Packages like ggplot2 make plotting easier and more customizable in R than in Python. Python is catching up, particularly in the area of interactive plots with packages like Bokeh, but has a way to go.

The bottom line

Performing data analysis tasks in either language is more similar than you might expect. As long as you understand the underlying concepts, pick the language that you’re most familiar with.

R has an edge in statistics and visualization, whereas Python has an advantage in machine learning and building tools.

If you’re new to data analysis, I’d advise learning Python, because it’s more straightforward and more versatile, but I’d also advise focusing on the concepts and quality of the analysis over language. At Dataquest, we teach data science by focusing on the concepts and helping you build projects and add value.

I personally like where tools like Jupyter Notebook and Beaker Notebook are headed in terms of letting you use either language, sometimes in the same analysis.

This article is from [Quora](https://www.quora.com/Which-is-better-for-data-analysis-R-or-Python)