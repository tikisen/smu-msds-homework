---
title: "Live Session 3 Assignment"
author: "TQ Senkungu"
date: "5/30/2018"
output:
    html_document:
        keep_md: true
---



## Titanic Data

I'm going to read the titanic data into R.

Then I take the count of the number of males and females and plot their frequency. Finally, I output the mean age, survival rate and the average fare paid in a table.


```r
setwd("~/Dropbox/Senkungu Fam/Education/SMU/Courses/MSDS 6306 Doing Data Science/GitHub Repo/6306-homework/awesome-public-datasets/Datasets")
df <- read.csv(file = "titanic.csv", header = TRUE)
women_count <- length(which(df$Sex == "female"))
men_count <- length(which(df$Sex == "male"))
women_count
```

```
## [1] 314
```

```r
men_count
```

```
## [1] 577
```

```r
barplot(c(men_count, women_count), names.arg = c("# of Men", "# of Women"), ylab = "Total Number", xlab = "Gender", main = "Number of Men and Women on the Titanic")
```

![](Tsenkungu_Livesession3assignment_files/figure-html/titanic-1.png)<!-- -->

```r
#head(df) #used to get a list of data and types
mean_subset <- df[c("Age","Survived","Fare")]
sapply(mean_subset,mean, na.rm=TRUE) #tricky tricky
```

```
##        Age   Survived       Fare 
## 29.6991176  0.3838384 32.2042080
```

```r
#mean(df$Age, na.rm = TRUE) #testing mean function
```

## Sleep Data

Here I created a function that takes the input of a table of data on sleep and outputs the median age, the average and standard deviation of self esteem and gives the range of the duration of sleep.


```r
setwd("~/Dropbox/Senkungu Fam/Education/SMU/Courses/MSDS 6306 Doing Data Science/GitHub Repo/6306-homework/unit03")
df_sleep <- read.csv(file = "sleep_data_01.csv", header = TRUE)
#head(df_sleep, 10) #used to get a list of data and types
sleep_report <- function(sleep_ages, sleep_durations, sleep_RSESs){
    sleep_median_age <- median(sleep_ages, na.rm = TRUE)
    sleep_min_duration <- min(sleep_ages, na.rm = TRUE)
    sleep_max_duration <- max(sleep_ages, na.rm = TRUE)
    sleep_mean_RSES <- mean(sleep_RSESs, na.rm = TRUE)
    sleep_sd_RSES <- sd(sleep_RSESs, na.rm = TRUE)
    sleep_report_df <- data.frame("MedianAge" = sleep_median_age, "SelfEsteem" = sleep_mean_RSES/5, "SE_SD" = sleep_sd_RSES/5, "DurationRange" = sleep_max_duration-sleep_min_duration)
    sleep_report_df <- sapply(sleep_report_df, round, digits=2)
    return(sleep_report_df)
}
sleep_report(df_sleep$Age, df_sleep$Duration, df_sleep$RSES)
```

```
##     MedianAge    SelfEsteem         SE_SD DurationRange 
##         14.00          3.62          1.24          6.00
```
