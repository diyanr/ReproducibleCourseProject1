---
title: "Reproducible Course Project 1"
output: html_document
---

## Loading the needed libraries    
Below are the libraries needed:  

<div class="chunk" id="unnamed-chunk-1"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl kwd">library</span><span class="hl std">(dplyr)</span>
</pre></div>
</div></div>

## Loading and preprocessing the data  
Below is code that is needed to:  

1. Load the data  

<div class="chunk" id="unnamed-chunk-2"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">activity</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">read.csv</span><span class="hl std">(</span><span class="hl str">&quot;activity.csv&quot;</span><span class="hl std">)</span>
</pre></div>
</div></div>

2. Process/transform the data  

<div class="chunk" id="unnamed-chunk-3"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">activity</span><span class="hl opt">$</span><span class="hl std">date</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">as.Date</span><span class="hl std">(activity</span><span class="hl opt">$</span><span class="hl std">date,</span> <span class="hl str">&quot;%Y-%m-%d&quot;</span><span class="hl std">)</span>
</pre></div>
</div></div>

## What is mean total number of steps taken per day?  
For this part of the assignment, I am ignoring the missing values in the dataset.  

1. Calculate the total number of steps taken per day  

<div class="chunk" id="unnamed-chunk-4"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">dailyTotalSteps</span> <span class="hl kwb">&lt;-</span> <span class="hl std">activity</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">group_by</span><span class="hl std">(date)</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">summarise</span><span class="hl std">(</span><span class="hl kwc">total</span> <span class="hl std">=</span> <span class="hl kwd">sum</span><span class="hl std">(steps))</span>
</pre></div>
</div></div>

2. Make a histogram of the total number of steps taken each day  

<div class="chunk" id="daily-total"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl kwd">with</span><span class="hl std">(dailyTotalSteps,</span> <span class="hl kwd">hist</span><span class="hl std">(total,</span> <span class="hl kwc">main</span> <span class="hl std">=</span> <span class="hl str">&quot;Daily Total&quot;</span><span class="hl std">))</span>
</pre></div>
<div class="rimage default"><img src="figure/daily-total-1.png" title="plot of chunk daily-total" alt="plot of chunk daily-total" class="plot" /></div>
</div></div>

3. Calculate the mean and median of the total number of steps taken per day  

<div class="chunk" id="unnamed-chunk-5"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl kwd">mean</span><span class="hl std">(dailyTotalSteps</span><span class="hl opt">$</span><span class="hl std">total,</span> <span class="hl kwc">na.rm</span> <span class="hl std">=</span> <span class="hl num">TRUE</span><span class="hl std">)</span>
</pre></div>
<div class="output"><pre class="knitr r">## [1] 10766.19
</pre></div>
<div class="source"><pre class="knitr r"><span class="hl kwd">median</span><span class="hl std">(dailyTotalSteps</span><span class="hl opt">$</span><span class="hl std">total,</span> <span class="hl kwc">na.rm</span> <span class="hl std">=</span> <span class="hl num">TRUE</span><span class="hl std">)</span>
</pre></div>
<div class="output"><pre class="knitr r">## [1] 10765
</pre></div>
</div></div>

## What is the average daily activity pattern?  

1. Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)  

<div class="chunk" id="daily-average"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">intervalAveSteps</span> <span class="hl kwb">&lt;-</span> <span class="hl std">activity</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">group_by</span><span class="hl std">(interval)</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">summarise</span><span class="hl std">(</span><span class="hl kwc">average</span> <span class="hl std">=</span> <span class="hl kwd">mean</span><span class="hl std">(steps,</span> <span class="hl kwc">na.rm</span> <span class="hl std">=</span> <span class="hl num">TRUE</span><span class="hl std">))</span>
<span class="hl kwd">with</span><span class="hl std">(intervalAveSteps,</span> <span class="hl kwd">plot</span><span class="hl std">(interval, average,</span> <span class="hl kwc">type</span> <span class="hl std">=</span> <span class="hl str">&quot;l&quot;</span><span class="hl std">,</span> <span class="hl kwc">main</span> <span class="hl std">=</span> <span class="hl str">&quot;Daily Average&quot;</span><span class="hl std">))</span>
</pre></div>
<div class="rimage default"><img src="figure/daily-average-1.png" title="plot of chunk daily-average" alt="plot of chunk daily-average" class="plot" /></div>
</div></div>

2. Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?  

<div class="chunk" id="unnamed-chunk-6"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">intervalAveSteps</span><span class="hl opt">$</span><span class="hl std">interval[intervalAveSteps</span><span class="hl opt">$</span><span class="hl std">average</span> <span class="hl opt">==</span> <span class="hl kwd">max</span><span class="hl std">(intervalAveSteps</span><span class="hl opt">$</span><span class="hl std">average)]</span>
</pre></div>
<div class="output"><pre class="knitr r">## [1] 835
</pre></div>
</div></div>

## Imputing missing values  

1. Calculate and report the total number of missing values in the dataset  

<div class="chunk" id="unnamed-chunk-7"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl kwd">sum</span><span class="hl std">(</span><span class="hl kwd">is.na</span><span class="hl std">(activity</span><span class="hl opt">$</span><span class="hl std">steps))</span>
</pre></div>
<div class="output"><pre class="knitr r">## [1] 2304
</pre></div>
</div></div>

2. Devise a strategy for filling in all of the missing values in the dataset.  

<div class="chunk" id="unnamed-chunk-8"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">imputeStep</span> <span class="hl kwb">&lt;-</span> <span class="hl kwa">function</span><span class="hl std">(</span><span class="hl kwc">step</span><span class="hl std">,</span> <span class="hl kwc">interval</span><span class="hl std">){</span>
  <span class="hl kwa">if</span><span class="hl std">(</span><span class="hl kwd">is.na</span><span class="hl std">(step)) {</span>
    <span class="hl kwd">round</span><span class="hl std">(intervalAveSteps</span><span class="hl opt">$</span><span class="hl std">average[intervalAveSteps</span><span class="hl opt">$</span><span class="hl std">interval</span> <span class="hl opt">==</span> <span class="hl std">interval])</span>
  <span class="hl std">}</span> <span class="hl kwa">else</span> <span class="hl std">{</span>
    <span class="hl std">step</span>
  <span class="hl std">}</span>
<span class="hl std">}</span>
</pre></div>
</div></div>

3. Create a new dataset that is equal to the original dataset but with the missing data filled in.  

<div class="chunk" id="unnamed-chunk-9"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">newActivity</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">mutate</span><span class="hl std">(activity,</span> <span class="hl kwc">steps</span> <span class="hl std">=</span> <span class="hl kwd">mapply</span><span class="hl std">(imputeStep, steps, interval))</span>
</pre></div>
</div></div>

4. Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day.  


<div class="chunk" id="daily-imputed-total"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">newDailyTotalSteps</span> <span class="hl kwb">&lt;-</span> <span class="hl std">newActivity</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">group_by</span><span class="hl std">(date)</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">summarise</span><span class="hl std">(</span><span class="hl kwc">total</span> <span class="hl std">=</span> <span class="hl kwd">sum</span><span class="hl std">(steps))</span>
<span class="hl kwd">with</span><span class="hl std">(newDailyTotalSteps,</span> <span class="hl kwd">hist</span><span class="hl std">(total,</span> <span class="hl kwc">main</span> <span class="hl std">=</span> <span class="hl str">&quot;Daily Imputed Total&quot;</span><span class="hl std">))</span>
</pre></div>
<div class="rimage default"><img src="figure/daily-imputed-total-1.png" title="plot of chunk daily-imputed-total" alt="plot of chunk daily-imputed-total" class="plot" /></div>
<div class="source"><pre class="knitr r"><span class="hl kwd">mean</span><span class="hl std">(newDailyTotalSteps</span><span class="hl opt">$</span><span class="hl std">total,</span> <span class="hl kwc">na.rm</span> <span class="hl std">=</span> <span class="hl num">TRUE</span><span class="hl std">)</span>
</pre></div>
<div class="output"><pre class="knitr r">## [1] 10765.64
</pre></div>
<div class="source"><pre class="knitr r"><span class="hl kwd">median</span><span class="hl std">(newDailyTotalSteps</span><span class="hl opt">$</span><span class="hl std">total,</span> <span class="hl kwc">na.rm</span> <span class="hl std">=</span> <span class="hl num">TRUE</span><span class="hl std">)</span>
</pre></div>
<div class="output"><pre class="knitr r">## [1] 10762
</pre></div>
</div></div>

## Are there differences in activity patterns between weekdays and weekends?  

1. Create a new factor variable in the dataset with two levels - "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.  

<div class="chunk" id="unnamed-chunk-10"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">makeFactor</span> <span class="hl kwb">&lt;-</span> <span class="hl kwa">function</span><span class="hl std">(</span><span class="hl kwc">date</span><span class="hl std">){</span>
  <span class="hl kwd">factor</span><span class="hl std">(</span><span class="hl kwd">weekdays</span><span class="hl std">(date)</span> <span class="hl opt">%in%</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl str">&quot;Saturday&quot;</span><span class="hl std">,</span><span class="hl str">&quot;Sunday&quot;</span><span class="hl std">),</span> <span class="hl kwc">levels</span> <span class="hl std">=</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl num">TRUE</span><span class="hl std">,</span><span class="hl num">FALSE</span><span class="hl std">),</span> <span class="hl kwc">labels</span> <span class="hl std">=</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl str">&quot;weekend&quot;</span><span class="hl std">,</span><span class="hl str">&quot;weekday&quot;</span><span class="hl std">))</span>
<span class="hl std">}</span>
<span class="hl std">newActivity</span> <span class="hl kwb">&lt;-</span> <span class="hl kwd">mutate</span><span class="hl std">(newActivity,</span> <span class="hl kwc">dayOfWeek</span> <span class="hl std">=</span> <span class="hl kwd">makeFactor</span><span class="hl std">(date))</span>
</pre></div>
</div></div>

2. Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis).  

<div class="chunk" id="weekday-average"><div class="rcode"><div class="source"><pre class="knitr r"><span class="hl std">weekdayActivity</span> <span class="hl kwb">&lt;-</span> <span class="hl std">newActivity</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">filter</span><span class="hl std">(dayOfWeek</span> <span class="hl opt">==</span> <span class="hl str">&quot;weekday&quot;</span><span class="hl std">)</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">group_by</span><span class="hl std">(interval)</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">summarise</span><span class="hl std">(</span><span class="hl kwc">average</span> <span class="hl std">=</span> <span class="hl kwd">mean</span><span class="hl std">(steps))</span>

<span class="hl std">weekendActivity</span> <span class="hl kwb">&lt;-</span> <span class="hl std">newActivity</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">filter</span><span class="hl std">(dayOfWeek</span> <span class="hl opt">==</span> <span class="hl str">&quot;weekend&quot;</span><span class="hl std">)</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">group_by</span><span class="hl std">(interval)</span> <span class="hl opt">%&gt;%</span> <span class="hl kwd">summarise</span><span class="hl std">(</span><span class="hl kwc">average</span> <span class="hl std">=</span> <span class="hl kwd">mean</span><span class="hl std">(steps))</span>

<span class="hl kwd">par</span><span class="hl std">(</span><span class="hl kwc">mfrow</span> <span class="hl std">=</span> <span class="hl kwd">c</span><span class="hl std">(</span><span class="hl num">1</span><span class="hl std">,</span> <span class="hl num">2</span><span class="hl std">))</span>
<span class="hl kwd">with</span><span class="hl std">(weekdayActivity,</span> <span class="hl kwd">plot</span><span class="hl std">(interval, average,</span> <span class="hl kwc">type</span> <span class="hl std">=</span> <span class="hl str">&quot;l&quot;</span><span class="hl std">,</span> <span class="hl kwc">main</span> <span class="hl std">=</span> <span class="hl str">&quot;Weekday Average&quot;</span><span class="hl std">))</span>
<span class="hl kwd">with</span><span class="hl std">(weekendActivity,</span> <span class="hl kwd">plot</span><span class="hl std">(interval, average,</span> <span class="hl kwc">type</span> <span class="hl std">=</span> <span class="hl str">&quot;l&quot;</span><span class="hl std">,</span> <span class="hl kwc">main</span> <span class="hl std">=</span> <span class="hl str">&quot;Weekend Average&quot;</span><span class="hl std">))</span>
</pre></div>
<div class="rimage default"><img src="figure/weekday-average-1.png" title="plot of chunk weekday-average" alt="plot of chunk weekday-average" class="plot" /></div>
</div></div>




