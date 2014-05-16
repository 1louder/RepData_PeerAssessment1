# Reproducible Research: Peer Assessment 1


## Loading and preprocessing the data
The data for this report can be found at https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip.  

After downloading the data set, it is read into R to analyze it.


```r
dat <- read.csv("activity.csv")
```



## What is mean total number of steps taken per day?
Here is a histogram showing the frequencies of the individual's number of steps per day.  Entries of "NA" are ignored.  


```r
clean <- na.omit(dat)
days <- unique(clean$date)
daily <- c()
for (i in 1:length(days)) {
    daily <- append(daily, sum(subset(clean, clean$date == days[i])$steps))
}
hist(daily)
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 


The **mean** and **median** total number of steps taken per day can be calculated by looking at the daily totals tallied in the *daily* variable above.  Again, entries of "NA" are ignored.


```r
stepsMean <- mean(daily)
stepsMedian <- median(daily)
stepsMean
```

```
## [1] 10766
```

```r
stepsMedian
```

```
## [1] 10765
```


On days when data was collected, the individual in this case took an average of 10,766 steps per day with a median value of 10,765 steps.

## What is the average daily activity pattern?
The following plot displays the individual's average number of steps by 5-minute interval over the entire two months.  Entries of "NA" are once again omitted.  


```r
fiveMins <- split(clean, clean$interval)
val <- c()
mx <- c()
for (i in 1:length(unique(clean$interval))) {
    val <- append(val, sum(fiveMins[[i]]["steps"])/(length(days)))
    if (max(val) == sum(fiveMins[[i]]["steps"])/(length(days))) {
        mx <- unique(clean$interval)[i]
    }
}
plot(unique(clean$interval), val, type = "l", xlab = "Interval", ylab = "Average Steps")
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 


The interval with the highest average number of steps is displayed below, as well as its value:


```r
mx
```

```
## [1] 835
```

```r
max(val)
```

```
## [1] 206.2
```

```r

## Imputing missing values



## Are there differences in activity patterns between weekdays and weekends?
```
