Tom Lous  
13 Jan 2015  

# Quiz 2
## Question 1

What is the variance of the distribution of the average an IID draw of n observations from a population with mean $μ$ and variance $σ^2$.

### Answer

For large enough $n$, the distribution of $S_n$ is close to the normal distribution with mean $µ$ and variance $\frac{σ^2}{n}$


---

## Question 2

Suppose that diastolic blood pressures (DBPs) for men aged 35-44 are normally distributed with a mean of 80 (mm Hg) and a standard deviation of 10. About what is the probability that a random 35-44 year old has a DBP less than 70?

### Answer

Let $X$ be DBP. We want $P(X \leq 70)$ given that $X$ is $N(80, 10^2)$.


```r
targetDBP <- 70
μ <- 80
σ <- 10
percentage <- round(pnorm(targetDBP, mean = μ, sd = σ) * 100)
percentage
```

```
## [1] 16
```
---

## Question 3

Brain volume for adult women is normally distributed with a mean of about 1,100 cc for women with a standard deviation of 75 cc. What brain volume represents the 95th percentile?

### Answer

Let $x$ be the volume of the brain for adult women. We want $x$ so that $F(x) = 0.95$.


```r
quantile <- 0.95
μ <- 1100
σ <- 75
volume <- round(qnorm(quantile, mean = μ, sd = σ))
volume
```

```
## [1] 1223
```

---

## Question 4

Refer to the previous question. Brain volume for adult women is about 1,100 cc for women with a standard deviation of 75 cc. Consider the sample mean of 100 random adult women from this population. What is the 95th percentile of the distribution of that sample mean?

### Answer

Let $\bar X$ be the average sample mean for 100 randomly sampled women.

The standard error is $SE_{\bar X} = \frac{σ}{\sqrt{n}}$

$X$ is $N(1100, 75^2 / 100)$.


```r
quantile <- 0.95
μ <- 1100
σ <- 75
n <- 100
SE <- σ/sqrt(n)
round(qnorm(quantile, mean = μ, sd = SE))
```

```
## [1] 1112
```

---

## Question 5

You flip a fair coin 5 times, about what's the probability of getting 4 or 5 heads?

### Answer

Let $p=0.5$ and $X$ be binomial


```r
p <- 0.5
n <- 5
quantile <- 3 # 4 or 5 out of 5, with lower
probPercentage1 <- round(pbinom(quantile, size=n, prob=p, lower.tail = FALSE) * 100)
probPercentage1
```

```
## [1] 19
```

Alternativly use a binomial coefficient and add the seperate chances.

${n \choose k} = \frac{n!}{k!(n-k)!}$


```r
combinedProb <- p ^ n
choose4Prob <- choose(n, 4) * combinedProb
choose5Prob <- choose(n, 5) * combinedProb

probPercentage2 <- round((choose4Prob + choose5Prob) * 100)
probPercentage2
```

```
## [1] 19
```


---

## Question 6

The respiratory disturbance index (RDI), a measure of sleep disturbance, for a specific population has a mean of 15 (sleep events per hour) and a standard deviation of 10. They are not normally distributed. Give your best estimate of the probability that a sample mean RDI of 100 people is between 14 and 16 events per hour?

### Answer

The Central Limit Theorem (CLT) states that for a large enough sample size $n$, the distribution of the sample mean $\bar x$  will approach a normal distribution.


```r
μ <- 15
σ <- 10
n <- 100
SE <- σ/sqrt(n)

left <- 14
right <- 16

percentageLeft <- pnorm(left, mean = μ, sd = SE) * 100
percentageRight <- pnorm(right, mean = μ, sd = SE) * 100

probPercentage <- round(percentageRight - percentageLeft)
probPercentage
```

```
## [1] 68
```



---

## Question 7

Consider a standard uniform density. The mean for this density is .5 and the variance is 1 / 12. You sample 1,000 observations from this distribution and take the sample mean, what value would you expect it to be near?

### Answer

Intuitivly it should be 0.5, but let's check:


```r
quantile <- 0.5
μ <- 0.5
σ <- 1/12
n <- 1000
SE <- σ/sqrt(n)

qnorm(quantile, mean = μ, sd = SE)
```

```
## [1] 0.5
```


---

## Question 8

The number of people showing up at a bus stop is assumed to be Poisson with a mean of 5 people per hour. You watch the bus stop for 3 hours. About what's the probability of viewing 10 or fewer people?

### Answer

Let $X$ be the number of people in 3 hours then $X \sim Poisson(tλ) = Poisson(3 \times 5)$


```r
t <- 3
λ <- 5
quantile <- 10

probability <- round(ppois(quantile, lambda = t * λ), digits=2)
probability
```

```
## [1] 0.12
```

---

