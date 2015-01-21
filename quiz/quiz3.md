Tom Lous  
19 Jan 2015  

# Quiz 3
## Question 1

In a population of interest, a sample of 9 men yielded a sample average brain volume of 1,100cc and a standard deviation of 30cc. What is a 95% Student's T confidence interval for the mean brain volume in this new population?

### Answer

Assuming underlying data is iid gaussian

$\frac{\bar X - μ}{S / \sqrt{n}}$

follows Gosset's $t$ distibution with $n-1$ degrees of freedom

Interval $\bar X \pm t_{n-1} S / \sqrt{n}$, where $t_{n-1}$ is the relevant quantile


```r
n <- 9
μ <- 1100
σ <- 30
quantile = 0.975 # is 95% with 2.5% on both sides of the range
confidenceInterval = μ + c(-1, 1) * qt(quantile, df=n-1) * σ / sqrt(n)
confidenceInterval
```

```
## [1] 1077 1123
```

---

## Question 2

A diet pill is given to 9 subjects over six weeks. The average difference in weight (follow up - baseline) is -2 pounds. What would the standard deviation of the difference in weight have to be for the upper endpoint of the 95% T confidence interval to touch 0?

### Answer

Interval $CI_{up} = \bar X + t_{n-1} S / \sqrt{n}$, where $t_{n-1}$ is the relevant quantile

Rewritten, to get standard deviation: $S = \frac{CI_{up} - \bar X * \sqrt{n}}{t_{n-1}}$


```r
n <- 9
averageDifference <- -2
quantile = 0.975 # is 95% with 2.5% on both sides of the range
ci_up = 0
σ = (ci_up - averageDifference * sqrt(n))/qt(quantile, df=n-1)
round(σ, 2)
```

```
## [1] 2.6
```

---

## Question 3

In an effort to improve running performance, 5 runners were either given a protein supplement or placebo. Then, after a suitable washout period, they were given the opposite treatment. Their mile times were recorded under both the treatment and placebo, yielding 10 measurements with 2 per subject. The researchers intend to use a T test and interval to investigate the treatment. Should they use a paired or independent group T test and interval?

### Answer

* A paired interval
* You could use either
* It's necessary to use both
* **Independent groups, since all subjects were seen under both systems**

---

## Question 4

In a study of emergency room waiting times, investigators consider a new and the standard triage systems. To test the systems, administrators selected 20 nights and randomly assigned the new triage system to be used on 10 nights and the standard system on the remaining 10 nights. They calculated the nightly median waiting time (MWT) to see a physician. The average MWT for the new system was 3 hours with a variance of 0.60 while the average MWT for the old system was 5 hours with a variance of 0.68. Consider the 95% confidence interval estimate for the differences of the mean MWT associated with the new system. Assume a constant variance. What is the interval? Subtract in this order (New System - Old System).

### Answer

Independent group T intervals

A $(1 - a) \times 100%$ confidence interval for $μ_y - μ_x$ is

$\bar Y - \bar X \pm t_{n_x + n_y - 2, 1 - α/2} S_p\left(\frac{1}{n_x} + \frac{1}{n_y}\right)^{1/2}$

The pooled variance estimator is: 

$S_p^2 = \{(n_x - 1) S_x^2 + (n_y - 1) S_y^2\}/(n_x + n_y - 2)$

Rewritten for available variables:

$S_p = \sqrt{\{(n_x - 1) var_x + (n_y - 1) var_y\}/(n_x + n_y - 2)}$


```r
quantile = 0.975 # is 95% with 2.5% on both sides of the range

n_y <- 10 # nights new system
n_x <- 10 # nights old system
var_y <- 0.60 # variance old (sqrt of σ)
var_x <- 0.68 # variance old (sqrt of σ)
μ_y <- 3# average hours new system
μ_x <- 5# average hours old system

# calculate pooled standard deviation
σ_p <- sqrt(((n_x - 1) * var_x + (n_y - 1) * var_y)/(n_x + n_y - 2))

confidenceInterval <- μ_y - μ_x + c(-1, 1) * qt(quantile, df=n_y+n_x-2) * σ_p * (1 / n_x + 1 / n_y)^.5
round(confidenceInterval,2)
```

```
## [1] -2.75 -1.25
```
---
