---
title       : Slidify Wine App
subtitle    : Some Scientific Calculations about Wine
author      : Diane Clow
job         : Developing Data Products Final Project
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---


## What Is It

This app takes a scientific approach to examining what makes wine good.  The data is gathered from the UCI Machine Learning Repository listed as "Wine Quality Data Set" (http://archive.ics.uci.edu/ml/datasets/Wine+Quality).  All of the data provided in this data set are values that can be measured in the wine.  

 

There are two data sets in this analysis, one for Red Wine and another for White Wine.  Using this app you can explore the some of the different chemical volumes that might make a particular style of red or white wine better than the other.  There are lots of cases where the same chemical composition recieves different ratings depending on if its red or white.

 

The datas description of the wine: "The two datasets are related to red and white variants of the Portuguese "Vinho Verde" wine. Due to privacy and logistic issues, only physicochemical (inputs) and sensory (the output) variables are available (e.g. there is no data about grape types, wine brand, wine selling price, etc.)."

--- .class #id 

## Variables

Below are the list of variables avalable for both data sets.  The algorithm used in this application uses all of the variables, and solves for Quality.  Quality is a interger value of 1-10, rating how good the wine is.


```r
red <- read.csv("data/winequality-red.csv", sep=";")
colnames(red)
```

```
##  [1] "fixed.acidity"        "volatile.acidity"     "citric.acid"         
##  [4] "residual.sugar"       "chlorides"            "free.sulfur.dioxide" 
##  [7] "total.sulfur.dioxide" "density"              "pH"                  
## [10] "sulphates"            "alcohol"              "quality"
```

--- .class #id 

## Prediction Models

Different models were created for red and white wine though both used the same method.  I ran the following code to generate my models.


```r
mod_RF.red <- train(quality ~., method="rf", data = training.red, 
                    trControl = trainControl(method="cv", number = 4))

mod_RF.white <- train(quality ~., method="rf", data = training.white, 
                      trControl = trainControl(method="cv", number = 4))
```

Each forest had 500 trees and an OOB estamite of hte error rate of about 31 on each.

--- .class #id 

## Limitations

There are some noticable limitations in this model.  

- There is a lot more to examinng the quality of wine then the 11 variables found in this data set.

- The majority of the wines in the data set are rated as a 6, and the range of quality is only 3-8

- This is a very specific set of wine that is going to have lots of similarities
