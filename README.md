# NYC Data Analysis Jobs
![R](https://user-images.githubusercontent.com/87658966/138593917-df40a964-3216-40a9-ae3e-d7029723420a.png)

## Description
Source: [Kagle data - Data Analysis Jobs, Based on NYC Jobs - October 2021](https://www.kaggle.com/intelai/data-analysis-jobs?select=data_analysis_jobs.csv)

This dataset contains current job postings available on the City of New York’s official jobs site (http://www.nyc.gov/html/careers/html/search/search.shtml). Internal postings available to city employees and external postings available to the general public are included. The dataset is a csv file containing 851 observations and 23 variables as seen in this partial view below.

![Screenshot 2021-10-24 084209](https://user-images.githubusercontent.com/87658966/138594691-6cafcf10-c33f-48cf-bb28-776e2cc4c88a.png)

The objective was to use one or more TidyVerse packages, and demonstrate the capabilities of the selected TidyVerse package with the dataset.

## Loading Data in RStudio
1. Load the Tidyverse package was loaded and later the Reactable package for interactive table.
2. Import the data from file loacted in Github with "readr package" from Tidyverse package.
3. Retrieve and review the names attributes of the dataset with "names()" function.

## Performing the Analysis
_Dataset Question (1): How many job postings are Internal and External? What are the Levels and how many are available?_
1. Create a new data frame using existing data frame by extracting columns pertaining to the question (Level and Posting Type).
2. Combine with the function "count()" which performs both group-by and count rows in each group into a single function.
3. Perform tidy functions and create visualizations (table and plot).

_Dataset Question (2): What are the Business Titles categories which NYC hires Data Analysis to perform? Which Business Title has the highest demand for Data Analysis?_
1. Create a new data frame using existing data frame by extracting column pertaining to the question (Business Title).
2. Peform tidy function on data to change column to uppercase and build a table of the counts at each combination of factor levels.
3. Use the summary() command to view the data statistics and filter frequency for creating a graph. 

## Conclusion
Tidyverse packages used on this dataset are as follows:
1.  readr - Import data 
2.  dplyr - Perfom data manipulaton 
3.  ggplot - Create graphic representation of input data 

## Links to Source file
[Github](https://rpubs.com/blesned/vignette)

## RStudio Dataset Code
---
title: "Kagle Data - Tidyverse"
author: "Coffy Andrews-Guo"
date: "`r Sys.Date()`"
output: rmarkdown::html_vignette
vignette: >
  %\VignetteIndexEntry{Vignette Title}
  %\VignetteEngine{knitr::rmarkdown}
  %\VignetteEncoding{UTF-8}
---

```{r setup, include = FALSE}
knitr::opts_chunk$set(
  fig.width = 7,
  fig.height = 3,
  collapse = TRUE,
  comment = "#>"
)
```

Source: [Kagle data - Data Analysis Jobs, Based on NYC Jobs - October 2021](https://www.kaggle.com/intelai/data-analysis-jobs?select=data_analysis_jobs.csv)

This dataset contains current job postings available on the City of New York’s official jobs site ( http://www.nyc.gov/html/careers/html/search/search.shtml ). Internal postings available to city employees and external postings available to the general public are included.


## Load Packages
```{r}
library("tidyverse")
library("reactable")
```



## Data Set

The `readr package` in tidyverse library contains the function `read_csv` that will import data from a csv file. The csv file was downloaded from Kaggle.com dataset on Data Analysis Jobs in NYC for October 2021. The imported data was read in to RStudio as a dataframe, `da`.  
```{r}
da <- read_csv("https://github.com/candrewxs/Vignettes/blob/master/dadata/data_analysis_jobs.csv?raw=true")
```



Retrieve the names attribute of the da data set with the `names()` function.
```{r}
names(da)
```

## Group by Variables

### Dataset Question: How many job postings are Internal and External? What are the Levels and how many are available?

Create a new data frame using existing data frame (da) by extracting columns: Level and Posting Type. The `count()` combines `group_by` and `count rows in each group` into a single function. Renamed the column name "n" to "Count" and created an interactive data table. 
```{r}
plot1 <- da %>%
   count(Level, `Posting Type`)  # dplyr package: group and count 

colnames(plot1)[3] <- "Count" 
# use function colnames() to rename column 
# and access individual column names with colnames(df)[index]

reactable(plot1) # interactive data table
```

### Visualization 
```{r}
# discrete visualization with ggplot2
p1 <- ggplot(data = plot1) 
  p1 + geom_col(aes(Level, Count, fill = `Posting Type`))
```


### Dataset Question: What are the Business Titles categories which NYC hires Data Analysis to perform? Which Business Title has the highest demand for Data Analysis?

Create a new data frame using existing data frame (da) by extracting column: Business Title. Tidy data frame column to upper case and build a contingency table of the counts at each combination of factor levels with the `table()` function. Renamed the column name "pl2" to "Business Title" and created an interactive data table showing the frequency. 
```{r}
plot2 <- as.data.frame(da[,5])

plot2$`Business Title` <- toupper(plot2$`Business Title`)

pl2 <- as.data.frame(table(plot2))

colnames(pl2)[1] <- "Business Title"

reactable(pl2)
```


```{r}
summary(pl2) # calculates some statistics on the data
```

Filter Business Titles with a frequency greater or equal to 10.  
```{r}
pl_2 <- filter(pl2, Freq >= 10) 

pl_2
```

### Visualization 
```{r}
p2 <- ggplot(pl_2) 
  p2 + geom_col(aes(`Business Title`, Freq)) +
    coord_flip()
```

## Conclusion
Kagle data - Data Analysis Jobs, Based on NYC Jobs was loaded and analyzed using R base functions and packages from Tidyverse and Reactable. These are the Tidyverse packages that were utilized to load `(readr)` , perfom data manipulaton `(dplyr)` , create graphic representation of input data `(ggplot2)`.



Links
[GitHub](https://rpubs.com/blesned/vignette)
