---
title: 'Reproducible Research: Peer Assessment 1'
output:
  html_document:
    keep_md: yes
  pdf_document: default
---
Reproducible Research - Project 1
==================================
# Loading and preprocessing the data

**- First, load the packages used in this analysis:**

```r
library(tidyverse)
```

```
## ── Attaching packages ────────────────────────────────────────────── tidyverse 1.3.0 ──
```

```
## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
## ✓ tidyr   1.1.1     ✓ stringr 1.4.0
## ✓ readr   1.3.1     ✓ forcats 0.5.0
```

```
## ── Conflicts ───────────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(formattable)
library(lubridate)
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

**- Load the data (i.e. read.csv())**

Set working directory to where data and R program lives:

```r
setwd("/Users/Wood/Desktop/Data_Science/Reproducible Research/Course Project 1/")
```

Read in the activity.csv data to "activitydata"; yields 17,568 obs of 3 variables:

```r
activitydata <- read.csv("activity.csv")
```

**- Process/transform the data (if necessary) into a format suitable for your analysis**
Looking at the data characteristics:

```r
str(activitydata)
```

```
## 'data.frame':	17568 obs. of  3 variables:
##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
##  $ date    : chr  "2012-10-01" "2012-10-01" "2012-10-01" "2012-10-01" ...
##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...
```

Change the date column from character to to a date format:

```r
activitydata$date <- ymd(activitydata$date)
```

# What is mean total number of steps taken per day?  (For this part of the assignment, you can ignore the missing values in the dataset.)

Calculate the total number of steps taken per day

```r
totalsteps <- aggregate(steps ~ date, activitydata, sum)
```

A table to show how many steps were taken on each day:

```r
formattable(totalsteps)
```


<table class="table table-condensed">
 <thead>
  <tr>
   <th style="text-align:right;"> date </th>
   <th style="text-align:right;"> steps </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:right;"> 2012-10-02 </td>
   <td style="text-align:right;"> 126 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-03 </td>
   <td style="text-align:right;"> 11352 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-04 </td>
   <td style="text-align:right;"> 12116 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-05 </td>
   <td style="text-align:right;"> 13294 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-06 </td>
   <td style="text-align:right;"> 15420 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-07 </td>
   <td style="text-align:right;"> 11015 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-09 </td>
   <td style="text-align:right;"> 12811 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-10 </td>
   <td style="text-align:right;"> 9900 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-11 </td>
   <td style="text-align:right;"> 10304 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-12 </td>
   <td style="text-align:right;"> 17382 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-13 </td>
   <td style="text-align:right;"> 12426 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-14 </td>
   <td style="text-align:right;"> 15098 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-15 </td>
   <td style="text-align:right;"> 10139 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-16 </td>
   <td style="text-align:right;"> 15084 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-17 </td>
   <td style="text-align:right;"> 13452 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-18 </td>
   <td style="text-align:right;"> 10056 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-19 </td>
   <td style="text-align:right;"> 11829 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-20 </td>
   <td style="text-align:right;"> 10395 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-21 </td>
   <td style="text-align:right;"> 8821 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-22 </td>
   <td style="text-align:right;"> 13460 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-23 </td>
   <td style="text-align:right;"> 8918 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-24 </td>
   <td style="text-align:right;"> 8355 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-25 </td>
   <td style="text-align:right;"> 2492 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-26 </td>
   <td style="text-align:right;"> 6778 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-27 </td>
   <td style="text-align:right;"> 10119 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-28 </td>
   <td style="text-align:right;"> 11458 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-29 </td>
   <td style="text-align:right;"> 5018 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-30 </td>
   <td style="text-align:right;"> 9819 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-10-31 </td>
   <td style="text-align:right;"> 15414 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-02 </td>
   <td style="text-align:right;"> 10600 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-03 </td>
   <td style="text-align:right;"> 10571 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-05 </td>
   <td style="text-align:right;"> 10439 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-06 </td>
   <td style="text-align:right;"> 8334 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-07 </td>
   <td style="text-align:right;"> 12883 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-08 </td>
   <td style="text-align:right;"> 3219 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-11 </td>
   <td style="text-align:right;"> 12608 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-12 </td>
   <td style="text-align:right;"> 10765 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-13 </td>
   <td style="text-align:right;"> 7336 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-15 </td>
   <td style="text-align:right;"> 41 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-16 </td>
   <td style="text-align:right;"> 5441 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-17 </td>
   <td style="text-align:right;"> 14339 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-18 </td>
   <td style="text-align:right;"> 15110 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-19 </td>
   <td style="text-align:right;"> 8841 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-20 </td>
   <td style="text-align:right;"> 4472 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-21 </td>
   <td style="text-align:right;"> 12787 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-22 </td>
   <td style="text-align:right;"> 20427 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-23 </td>
   <td style="text-align:right;"> 21194 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-24 </td>
   <td style="text-align:right;"> 14478 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-25 </td>
   <td style="text-align:right;"> 11834 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-26 </td>
   <td style="text-align:right;"> 11162 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-27 </td>
   <td style="text-align:right;"> 13646 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-28 </td>
   <td style="text-align:right;"> 10183 </td>
  </tr>
  <tr>
   <td style="text-align:right;"> 2012-11-29 </td>
   <td style="text-align:right;"> 7047 </td>
  </tr>
</tbody>
</table>

**- If you do not understand the difference between a histogram and a barplot, research the difference between them. Make a histogram of the total number of steps taken each day**

```r
hist(totalsteps$steps,
        main = "Histogram of Total Number of Steps per Day",
        xlab = "Total Steps per day",
        ylab = "Frequency")
```

![](PA1_template_files/figure-html/unnamed-chunk-7-1.png)<!-- -->

**- Calculate and report the mean and median of the total number of steps taken per day**

```r
meansteps <- mean(totalsteps$steps)
meansteps
```

```
## [1] 10766.19
```


```r
mediansteps <- median(totalsteps$steps)
mediansteps
```

```
## [1] 10765
```

# What is the average daily activity pattern?

**- Make a time series plot (i.e. type = "l") if the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)**

```r
meanstepsbyinterval <- aggregate(steps ~ interval, activitydata, mean)

plot(x=meanstepsbyinterval$interval, y=meanstepsbyinterval$steps,
        type="l",
        xlab = "5-minute Interval Over the Day",
        ylab = "Average Number of Steps")
```

![](PA1_template_files/figure-html/unnamed-chunk-10-1.png)<!-- -->

**- Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?**

```r
max(meanstepsbyinterval$steps)
```

```
## [1] 206.1698
```
Interval 835 has the maximum AVERAGE number of steps (206.1698113).

# Imputing missing values
Note that there are a number of days/intervals where there are missing values (coded as NA). The presence of missing days may introduce bias into some calculations or summaries of the data.

**- Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)**

```r
sum(is.na(activitydata$steps))  
```

```
## [1] 2304
```

```r
sum(is.na(activitydata$date))  
```

```
## [1] 0
```

```r
sum(is.na(activitydata$interval))  
```

```
## [1] 0
```

**- Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.**

Strategy is to replace missing values in the dataset with the median for that day.

**- Create a new dataset that is equal to the original dataset but with the missing data filled in.**

The new dataset is called "activitydataclean":

```r
activitydataclean <- activitydata
activitydataclean <- activitydataclean %>% 
        mutate(steps=replace(steps, is.na(steps), median(steps, na.rm=TRUE)))
```

**- Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?**

Calculate the total number of steps per day with the clean data set.

```r
totalstepsclean <- aggregate(steps ~ date, activitydataclean, sum)

meanstepsclean <- mean(totalstepsclean$steps)
#    10,766.19

medianstepsclean <- median(totalstepsclean$steps)
#    10,765
```

Create the plot:  

```r
par(mfrow=c(1,2))
hist(totalstepsclean$steps, breaks = 20,
        main = "Clean Data",
        xlab = "Total Steps per day",
        ylab = "Frequency")
        
hist(totalsteps$steps, breaks = 20,
        main = "Original Data",
        xlab = "Total Steps per day",
        ylab = "Frequency")  
```

![](PA1_template_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

The impact of our cleaning strategy is that the intervals that capture between 0 and 1,000 steps per day.  

# Are there differences in activity patterns between weekdays and weekends?
For this part the weekdays() function may be of some help here. Use the dataset with the filled-in missing values for this part.

**- Create a new factor variable in the dataset with two levels – “weekday” and “weekend” indicating whether a given date is a weekday or weekend day.**

```r
activitydataclean$weekday <- factor(weekdays(activitydataclean$date))
levels(activitydataclean$weekday) <- list("Weekend"=c("Saturday","Sunday"),
        "Weekday"=c("Monday","Tuesday","Wednesday","Thursday","Friday"))
```

**- Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.**

Subset the data into Weekend and Weekday buckets:

```r
weekenddata <- subset(activitydataclean, weekday=="Weekend")
weekdaydata <- subset(activitydataclean, weekday=="Weekday")

weekendmeansteps <- aggregate(steps ~ interval, weekenddata, mean)
weekdaymeansteps <- aggregate(steps ~ interval, weekdaydata, mean)
```

Now make the plot:

```r
par(mfrow=c(2,1))
plot(x=weekendmeansteps$interval, y=weekendmeansteps$steps,
        type="l",
        xlab = "5-minute Interval Over the Day (Weekend)",
        ylab = "Weekend Average Number of Steps",
        ylim=c(0,225))

plot(x=weekdaymeansteps$interval, y=weekdaymeansteps$steps,
        type="l",
        xlab = "5-minute Interval Over the Day (Weekday)",
        ylab = "Weekday Average Number of Steps",
        ylim=c(0,225))
```

![](PA1_template_files/figure-html/unnamed-chunk-18-1.png)<!-- -->
