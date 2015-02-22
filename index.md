---
title       : Compound Interest App
subtitle    : Computes Compound Interest
author      : Willy Cass
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : mathjax            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## What It Does

* This app calculates the amount of money in an account at a certain time based on 
compound interest.  
* The principle is the amount in the account on the start date. 
* The annual interest rate is the rate ofincrease of the principle, in percent per year, not taking into account compounding. 

---

## What It Does (Continued)
* The number of compounding periods is the number of times per year the amount of interest 
from the last period is computed and then added to the total. 
* The start and end dates define the period of time over which the interest accrues.
* The algorithm computes interest based on the number of completed periods between
the dates. 
* The periods starting on the start date and having a length of 365.25
divided by number of periods per year. 
* The rate of increase for each period is the annual rate divided by the number of periods per year. 
* The overall increase in the account balance and the value and difference for continuous compounding are also given.

---

## Example

* Suppose I have $10,000 on 1/1/2015
* I put it in a savings account with an interest rate of 2.5%
* Interest in the account is compounded 4 times a year
* What will my balance be on 1/2/2030? 
* The code on the next slide shows how this can be calculated in R
* The app uses similar code to calculate compound interest, with controls for the variables!

---

## Example (Continued)


```r
principle <- 10000  #starting amount
r <- .025           #Interest rate, as a fraction
n <- 4              #Number of compounding periods per year
t0 <- as.Date('2015-01-01') #start date
t1 <- as.Date('2030-01-02') #end date
t.days <- t1 - t0
t <- as.numeric(t.days/365.25) #convert time to years
balance <- principle * (1 + r/n) ^ (trunc(t * n))
interest <- balance - principle
balance.cont <- principle * exp(r*t)
interest.cont <- balance.cont - principle
```

#### The balance: $1.4532944 &times; 10<sup>4</sup>
#### The interest: $4532.9440828
#### The balance (continuous compounding): $1.4551159 &times; 10<sup>4</sup>
#### The interest (continuous compounding): $4551.1590586
