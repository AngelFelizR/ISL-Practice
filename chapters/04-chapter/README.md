04-execises
================

- <a href="#conceptual" id="toc-conceptual"><span
  class="toc-section-number">1</span> Conceptual</a>
- <a href="#applied" id="toc-applied"><span
  class="toc-section-number">2</span> Applied</a>

## Conceptual

1.  **Using a little bit of algebra, prove that (4.2) is equivalent to
    (4.3). In other words, the logistic function representation and
    logit representation for the logistic regression model are
    equivalent.**

$$
\begin{split}
p(X) &= \frac{e^{\beta_{0}+\beta_{1}X}}
            {1+e^{\beta_{0}+\beta_{1}X}} \\
p(X) (1+e^{\beta_{0}+\beta_{1}X}) & = e^{\beta_{0}+\beta_{1}X} \\
p(X)+p(X) e^{\beta_{0}+\beta_{1}X} & = e^{\beta_{0}+\beta_{1}X} \\
p(X) & = e^{\beta_{0}+\beta_{1}X} - p(X) e^{\beta_{0}+\beta_{1}X} \\
p(X) & = (1 - p(X))e^{\beta_{0}+\beta_{1}X} \\
\frac{p(X)}{1 - p(X)} & = e^{\beta_{0}+\beta_{1}X}
\end{split}
$$

2.  **It was stated in the text that classifying an observation to the
    class for which (4.17) is largest is equivalent to classifying an
    observation to the class for which (4.18) is largest. Prove that
    this is the case. In other words, under the assumption that the
    observations in the kth class are drawn from a N(µk,σ2)
    distribution, the Bayes classiﬁer assigns an observation to the
    class for which the discriminant function is maximized.**

To prove that both functions would provide the same class we need to
check that both functions change from one $Y$ class to other in the same
$x$ value.

If $K = 2$ and $\pi_1 = \pi_2 = \pi_c$ we can show that:

$$
\begin{split}
p_{1}(x) & = p_{2}(x) \\
\frac{\pi_c \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{1}{2\sigma^2} (x - \mu_{1})^2}}
     {\sum_{l=1}^{K} 
      \pi_l \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{1}{2\sigma^2} (x - \mu_{l})^2}}
& = 
\frac{\pi_c \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{1}{2\sigma^2} (x - \mu_{2})^2}}
     {\sum_{l=1}^{K} 
      \pi_l \frac{1}{\sqrt{2\pi} \sigma} e^{-\frac{1}{2\sigma^2} (x - \mu_{l})^2}} \\
e^{-\frac{1}{2\sigma^2} (x - \mu_{1})^2} 
& = 
e^{-\frac{1}{2\sigma^2} (x - \mu_{2})^2} \\
\frac{e^{-\frac{1}{2\sigma^2} (x - \mu_{1})^2}}{e^{-\frac{1}{2\sigma^2} (x - \mu_{2})^2}}
& = 1 \\
(x - \mu_{2})^2 - (x - \mu_{1})^2 
& = 0 \\
x^2 - 2x\mu_{2} + \mu_{2}^2 - (x^2 - 2x\mu_{1} + \mu_{1}^2)
& = 0 \\
2x (\mu_{1}- \mu_{2}) & = \mu_{1}^2 - \mu_{2}^2  \\
x & = \frac{\mu_{1}^2 - \mu_{2}^2}{2 (\mu_{1}- \mu_{2})} \\
x & = \frac{\mu_1 + \mu_2}{2}
\end{split}
$$

And also:

$$
\begin{split}
\delta_{1}(x) & = \delta_{2}(x) \\
\log{(\pi_{c})} 
- \frac{\mu_{1}^2}{2\sigma^2} 
+ x \cdot \frac{\mu_{1}}{\sigma^2} 
& =
\log{(\pi_{c})} 
- \frac{\mu_{2}^2}{2\sigma^2} 
+ x \cdot \frac{\mu_{2}}{\sigma^2} \\
x (\mu_{1} - \mu_{2}) & = \frac{\mu_{1}^2 - \mu_{2}^2}{2} \\
x & = \frac{\mu_{1}^2 - \mu_{2}^2}{2(\mu_{1} - \mu_{2})} \\
x & = \frac{\mu_1 + \mu_2}{2}
\end{split}
$$

Let’s see an example visually by setting as example the next values for
each $Y$ class:

| $k$ | $\sigma$ | $\pi$ | $\mu$ |
|:---:|:--------:|:-----:|:-----:|
|  1  |   0.5    |  0.5  |   2   |
|  2  |   0.5    |  0.5  |   4   |

``` r
library(ggplot2)
library(patchwork)

k_function <- function(x,
                       k,
                       sigma = c(0.5,0.5),
                       pi_k = c(0.5,0.5),
                       mu = c(2, 4),
                       logit = FALSE){
  
  if(logit){
    
    return(x * mu[k]/sigma[k]^2 - mu[k]^2/(2*sigma[k]^2) + log(pi_k[k]))
    
  }
  
  denominator <-
    sapply(x, \(y) sum(pi_k * (1/(sqrt(2*pi)*sigma)) * exp(-1/(2*sigma^2) * (y - mu)^2) ) )
  
  k_numerador <-
   (pi_k[k]* (sqrt(2*pi)*sigma[k])^-1 * exp(- (2*sigma[k]^2)^-1 * (x - mu[k])^2))
  
  return(k_numerador / denominator)
  
}

BasePlot <-
  data.frame(x = 1:5) |>
  ggplot(aes(x))+
  scale_x_continuous(breaks = scales::breaks_width(1))+
  theme_light()+
  theme(panel.grid.major.y = element_blank(),
        panel.grid.minor.y = element_blank(),
        axis.title.y = element_blank(),
        axis.text.y = element_blank(),
        axis.ticks.y = element_blank())
  
p1 <-
  BasePlot +
  geom_function(fun = \(y) k_function(x = y, k = 1), color = "blue")+
  geom_function(fun = \(y) k_function(x = y, k = 2), color = "red")

p2 <-
  BasePlot +
  geom_function(fun = \(y) k_function(x = y, k = 1, logit = TRUE), color = "blue")+
  geom_function(fun = \(y) k_function(x = y, k = 2, logit = TRUE), color = "red")


(p1 / p2) +
  plot_annotation(title = 'Comparing Proportion Function vs Logit Function of LDA',
                  theme = theme(plot.title = element_text(face = "bold")) )
```

![](04-execises_files/figure-commonmark/unnamed-chunk-1-1.png)

3.  **This problem relates to the QDA model, in which the observations
    within each class are drawn from a normal distribution with a class
    specific mean vector and a class specific covariance matrix. We
    consider the simple case where p = 1; i.e. there is only one
    feature. Suppose that we have K classes, and that if an observation
    belongs to the kth class then X comes from a one-dimensional normal
    distribution, X ∼ N(µk, σ2k). Recall that the density function for
    the one-dimensional normal distribution is given in (4.16). Prove
    that in this case, the Bayes classifier is not linear. Argue that it
    is in fact quadratic.**

$$
\begin{split}
p_k(x) & = 
\frac{\pi_k \frac{1}{\sqrt{2\pi} \sigma_k} e^{-\frac{1}{2\sigma_k^2} (x - \mu_{1})^2}}
     {\sum_{l=1}^{K} 
      \pi_l \frac{1}{\sqrt{2\pi} \sigma_l} e^{-\frac{1}{2\sigma_l^2} (x - \mu_{l})^2}} \\
& = 
\frac{\pi_k \frac{1}{\sqrt{2\pi} \sigma_k} e^{-\frac{1}{2\sigma_k^2} (x - \mu_{1})^2}}
     {\frac{1}{\sqrt{2\pi}} 
     \sum_{l=1}^{K}\pi_l \frac{1}{\sigma_l} e^{-\frac{1}{2\sigma_l^2} (x - \mu_{l})^2}} \\
& = 
\frac{\frac{\pi_k}{\sigma_k} e^{-\frac{1}{2\sigma_k^2} (x - \mu_{1})^2}}
     {\sum_{l=1}^{K} \frac{\pi_l}{\sigma_l} e^{-\frac{1}{2\sigma_l^2} (x - \mu_{l})^2}} \\
\end{split}
$$

As the denominator is a constant for any $k$, we can define:
$g(x) = \frac{1}{\sum_{l=1}^{K} \frac{\pi_l}{\sigma_l} e^{-\frac{1}{2\sigma_l^2} (x - \mu_{l})^2}}$

$$
\begin{split}
p_k(x) & = g(x) \frac{\pi_k}{\sigma_k} 
           e^{-\frac{1}{2\sigma_k^2} (x - \mu_{k})^2}\\
\log{(p_k(x))}& =
\log{\left( g(x) \frac{\pi_k}{\sigma_k} 
            e^{-\frac{1}{2\sigma_k^2} (x - \mu_{k})^2} \right)}\\
& =
\log{(g(x))} + \log{(\pi_k)} - \log{(\sigma_k)} -\frac{1}{2\sigma_k^2} (x - \mu_{k})^2 \\
& =
\log{(g(x))} + \log{(\pi_k)} - \log{(\sigma_k)} -\frac{\mu_k^2 - 2\mu_kx + x^2}{2\sigma_k^2} \\
& =
\left( \log{(g(x))} + \log{(\pi_k)} - \log{(\sigma_k)} - \frac{\mu_k^2}{2\sigma_k^2} \right) 
+ \frac{\mu_k}{\sigma_k^2} \cdot x - \frac{1}{2\sigma_k^2} \cdot x^2 \\
\end{split}
$$

4.  **When the number of features p is large, there tends to be a
    deterioration in the performance of KNN and other local approaches
    that perform prediction using only observations that are near the
    test observation for which a prediction must be made. This
    phenomenon is known as the *curse of dimensionality*, and it ties
    into the fact that non-parametric approaches often perform poorly
    when p is large. We will now investigate this curse.**

- **Suppose that we have a set of observations, each with measurements
  on p = 1 feature, X. We assume that X is uniformly (evenly)
  distributed on \[0, 1\]. Associated with each observation is a
  response value. Suppose that we wish to predict a test observation’s
  response using only observations that are within 10 % of the range of
  X closest to that test observation. For instance, in order to predict
  the response for a test observation with X = 0.6, we will use
  observations in the range \[0.55, 0.65\]. On average, what fraction of
  the available observations will we use to make the prediction?**

``` r
library(data.table)

set.seed(123)

UnifDistVar1 <-
  data.table(sample = 1:1000
  )[, .(x1 = runif(1000)),
    by = "sample"
  ][, .(prop = mean(x1 %between% c(0.6 - 0.1/2, 0.6 + 0.1/2))),
    by = "sample"]
  
mean(UnifDistVar1$prop)
```

    [1] 0.100297

- **Now suppose that we have a set of observations, each with
  measurements on p = 2 features, X1 and X2. We assume that (X1, X2) are
  uniformly distributed on \[0, 1\] × \[0, 1\]. We wish to predict a
  test observation’s response using only observations that are within 10
  % of the range of X1 and within 10 % of the range of X2 closest to
  that test observation. For instance, in order to predict the response
  for a test observation with X1 = 0.6 and X2 = 0.35, we will use
  observations in the range \[0.55, 0.65\] for X1 and in the range
  \[0.3, 0.4\] for X2. On average, what fraction of the available
  observations will we use to make the prediction?**

``` r
set.seed(123)

UnifDistVar2 <-
  UnifDistVar1[, .(x1 = runif(1000),
                   x2 = runif(1000)),
               by = "sample"
  ][ , .(prop = mean(x1 %between% c(0.6 - 0.1/2, 0.6 + 0.1/2) &
                     x2 %between% c(0.35 - 0.1/2, 0.35 + 0.1/2))),
     by = "sample"]

mean(UnifDistVar2$prop)
```

    [1] 0.009943

- **Now suppose that we have a set of observations on p = 100 features.
  Again the observations are uniformly distributed on each feature, and
  again each feature ranges in value from 0 to 1. We wish to predict a
  test observation’s response using observations within the 10 % of each
  feature’s range that is closest to that test observation. What
  fraction of the available observations will we use to make the
  prediction?**

``` r
0.1^100
```

    [1] 1e-100

- **Using your answers to parts (a)–(c), argue that a drawback of KNN
  when p is large is that there are very few training observations
  “near” any given test observation.**

As *p* gets lager every point has more specifications to meet and the
number of point which meet them decrease.

5.  **We now examine the differences between LDA and QDA.**

- **If the Bayes decision boundary is linear, do we expect LDA or QDA to
  perform better on the training set? On the test set?**

| Type of set to test |              Perform better               |
|:-------------------:|:-----------------------------------------:|
|    training set     |  ***QDA***, as it will model some noise   |
|      test set       | ***LDA***, as decision boundary is lineal |

- **If the Bayes decision boundary is non-linear, do we expect LDA or
  QDA to perform better on the training set? On the test set?**

| Type of set to test |                Perform better                 |
|:-------------------:|:---------------------------------------------:|
|    training set     |    ***QDA***, as it will model some noise     |
|      test set       | ***QDA***, as decision boundary is non-linear |

- **In general, as the sample size n increases, do we expect the test
  prediction accuracy of QDA relative to LDA to improve, decline, or be
  unchanged? Why?**

The test prediction accuracy won’t change by increasing *n*, as that
measure depends on the real shape of the *Bayes decision boundary*.

- **True or False: Even if the Bayes decision boundary for a given
  problem is linear, we will probably achieve a superior test error rate
  using QDA rather than LDA because QDA is flexible enough to model a
  linear decision boundary. Justify your answer.**

**FALSE**, as QDA would model some noise that could affect the
prediction accuracy.

6.  **Suppose we collect data for a group of students in a statistics
    class with variables X1 = hours studied, X2 = undergrad GPA, and Y =
    receive an A. We fit a logistic regression and produce estimated
    coefficient, $\hat{\beta}_0 = −6$, $\hat{\beta}_1 = 0.05$ and
    $\hat{\beta}_2 = 1$.**

- **Estimate the probability that a student who studies for 40 h and has
  an undergrad GPA of 3.5 gets an A in the class.**

``` r
LogisticCOef <- -6 + 0.05 * 40 + 1* 3.5

exp(LogisticCOef)/(1+exp(LogisticCOef))
```

    [1] 0.3775407

- **How many hours would the student in part (a) need to study to have a
  50 % chance of getting an A in the class?**

$$
\begin{split}
\log{ \left( \frac{p(X)}{1 - p(X)} \right)} & = \beta_{0}+\beta_{1}X_1+\beta_{2}X_2 \\
\log{ \left( \frac{0.5}{1 - 0.5} \right)} & = \beta_{0}+\beta_{1}X_1+\beta_{2}X_2 \\
0 & = \beta_{0}+\beta_{1}X_1+\beta_{2}X_2 \\
X_2 & = \frac{-\beta_0-\beta_{2}X_2}{\beta_{1}} \\
X_2 & = \frac{-(-6)-(1 \times 3.5)}{0.05}
\end{split}
$$

``` r
paste((6-3.5)/0.05, "horas")
```

    [1] "50 horas"

7.  **Suppose that we wish to predict whether a given stock will issue a
    dividend this year (“Yes” or “No”) based on X, last year’s percent
    profit. We examine a large number of companies and discover that the
    mean value of X for companies that issued a dividend was ¯X = 10,
    while the mean for those that didn’t was ¯X = 0. In addition, the
    variance of X for these two sets of companies was ˆσ2 = 36. Finally,
    80 % of companies issued dividends. Assuming that X follows a normal
    distribution, predict the probability that a company will issue a
    dividend this year given that its percentage profit was X = 4 last
    year.**

``` r
exp(log(0.80) - 10^2/(2*36) + 4 * 10/36) |> scales::percent(accuracy = 1)
```

    [1] "61%"

8.  **Suppose that we take a data set, divide it into equally-sized
    training and test sets, and then try out two different
    classification procedures. First we use logistic regression and get
    an error rate of 20 % on the training data and 30 % on the test
    data. Next we use 1-nearestbors (i.e. K = 1) and get an average
    error rate (averaged over both test and training data sets) of 18 %.
    Based on these results, which method should we prefer to use for
    classification of new observations? Why?**

We should use the KNN as it has a lower test error rate than the
logistic regression.

9.  **This problem has to do with odds.**

- **On average, what fraction of people with an odds of 0.37 of
  defaulting on their credit card payment will in fact default?**

$$
\begin{split}
\frac{p(X)}{1 - p(X)} & = Y \\
p(X) & = Y - Yp(X) \\
p(X) + Yp(X) & = Y \\
p(X) & = \frac{Y}{1+Y} = \frac{0.37}{1.37} = 0.27
\end{split}
$$

- **Suppose that an individual has a 16 % chance of defaulting on her
  credit card payment. What are the odds that she will default?**

``` r
0.16/(1-0.16)
```

    [1] 0.1904762

12. **Suppose that you wish to classify an observation X ∈ R into apples
    and oranges. You fit a logistic regression model and find that**

$$
\widehat{\text{Pr}}(Y = \text{orange}|X=x) =
\frac{\exp(\hat{\beta}_0+\hat{\beta}_1x)}
{1 + \exp(\hat{\beta}_0+\hat{\beta}_1x)}
$$

**Your friend fits a logistic regression model to the same data using
the softmax formulation in (4.13), and finds that**

$$
\widehat{\text{Pr}}(Y = \text{orange}|X=x) =
\frac{\exp(\hat{\alpha}_{\text{orange}0}+
           \hat{\alpha}_{\text{orange}1}x)}
{\exp(\hat{\alpha}_{\text{orange}0}+
      \hat{\alpha}_{\text{orange}1}x)+
 \exp(\hat{\alpha}_{\text{apple}0}+
      \hat{\alpha}_{\text{apple}1}x)}
$$

- **What is the log odds of orange versus apple in your model?**

$$
\log{
  \left( 
    \frac{\widehat{\text{Pr}}(Y = \text{orange}|X=x)}
         {1 - \widehat{\text{Pr}}(Y = \text{orange}|X=x)}
  \right)} = 
\hat{\beta}_0+\hat{\beta}_1x
$$

- **What is the log odds of orange versus apple in your friend’s
  model?**

$$
\log{
  \left( 
    \frac{\exp(\hat{\alpha}_{\text{orange}0} + \hat{\alpha}_{\text{orange}1}x)}
         {\exp(\hat{\alpha}_{\text{apple}0} + \hat{\alpha}_{\text{apple}1}x)}
  \right)} = 
(\hat{\alpha}_{\text{orange}0} - \hat{\alpha}_{\text{apple}0}) +
(\hat{\alpha}_{\text{orange}1} - \hat{\alpha}_{\text{apple}1}) x
$$

- **Suppose that in your model, $\hat{\beta}_0 = 2$ and
  $\hat{\beta}_1 = -1$. What are the coefficient estimates in your
  friend’s model? Be as specific as possible.**

$\hat{\beta}_0 = 2$ and $\hat{\beta}_1 = -1$

## Applied
