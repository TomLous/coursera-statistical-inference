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
