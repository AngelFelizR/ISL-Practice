03-execises
================

- <a href="#conceptual" id="toc-conceptual"><span
  class="toc-section-number">1</span> Conceptual</a>
- <a href="#applied" id="toc-applied"><span
  class="toc-section-number">2</span> Applied</a>

## Conceptual

1.  ***Describe the null hypotheses to which the p-values given in Table
    3.4 correspond. Explain what conclusions you can draw based on these
    p-values. Your explanation should be phrased in terms of sales, TV,
    radio, and newspaper, rather than in terms of the coefficients of
    the linear model.***

Null hypotheses for each predictor each coefficient is 0. We can see in
the table that we can reject the null hypotheses for **TV** and
**radio** but there isn’t enough evidence to reject the null hypotheses
for **newspaper**.

2.  ***Carefully explain the differences between the KNN classifier and
    KNN regression methods.***

The classifier assigns classes based on the most often class of the
closest $K$ elements, on the other hand the regression estimate each
value taking the mean of the closest $K$ elements.

3.  ***Suppose we have a data set with five predictors to predict the
    starting salary after graduation (in thousands of dollars) and after
    using least squares we fitted the next model:***

| Variable                                    | Coefficient              |
|:--------------------------------------------|:-------------------------|
| Level (High School)                         | $\hat{\beta}_{0} = 50$   |
| $X_{1}$ = GPA                               | $\hat{\beta}_{1} = 20$   |
| $X_{2}$ = IQ                                | $\hat{\beta}_{2} = 0.07$ |
| $X_{3}$ = Level (College)                   | $\hat{\beta}_{3} = 35$   |
| $X_{4}$ = Interaction between GPA and IQ    | $\hat{\beta}_{4} = 0.01$ |
| $X_{5}$ = Interaction between GPA and Level | $\hat{\beta}_{5} = −10$  |

- **Which answer is correct, and why?**\*

Based on this information we can say that:

> For a fixed value of IQ and GPA, college graduates earn more, on
> average, than high school graduate.

As High School students earn on average $\hat{\beta}_{0} = 50$ College
students earn \|$\hat{\beta}_{0} + \hat{\beta}_{3} = 85$

- ***Predict the salary of a college graduate with IQ of 110 and a GPA
  of 4.0.***

$$
\begin{split}
\hat{Y} & = 35 + 20 (4) + 0.07 (110) + 35 + 0.01(4)(110) - 10 (4) \\
        & = 122.1
\end{split}
$$

- ***True or false: Since the coefficient for the GPA/IQ interaction
  term is very small, there is very little evidence of an interaction
  effect. Justify your answer.***

FALSE, we can not make conclusions about the significance of any tern
about checking the the standard error of each term. The coefficient
might small because the IQ has very high values if we contrast the GPA
ones.

4.  ***I collect a set of data (n = 100 observations) containing a
    single predictor and a quantitative response. I then fit a linear
    regression model to the data, as well as a separate cubic
    regression,
    i.e. $Y = \beta_{0} + \beta_{1}x + \beta_{2}x^2 + \beta_{3}x^3 + \epsilon$.***

- ***Suppose that the true relationship between X and Y is linear,
  i.e. $Y = \beta_{0} + \beta_{1}x + \epsilon$. Consider the training
  residual sum of squares (RSS) for the linear regression, and also the
  training RSS for the cubic regression. Would we expect one to be lower
  than the other, would we expect them to be the same, or is there not
  enough information to tell? Justify your answer.***

As the training RSS always gets lower as we increase the flexibility the
cubic regression would have a lower RSS.

- \***Answer (a) using test rather than training RSS.**

The linear regression would have a lower test RSS, as it reduces de
scare bias of the model.

- ***Suppose that the true relationship between X and Y is not linear,
  but we don’t know how far it is from linear. Consider the training RSS
  for the linear regression, and also the training RSS for the cubic
  regression. Would we expect one to be lower than the other, would we
  expect them to be the same, or is there not enough information to
  tell? Justify your answer.***

As the training RSS always gets lower as we increase the flexibility the
cubic regression would have a lower RSS.

- \***Answer (c) using test rather than training RSS.**

The cubic regression would have a lower test RSS, as it reduces de scare
bias of the model.

5.  ***Consider the fitted values that result from performing linear
    regression without an intercept. In this setting, the $i$th fitted
    value takes the form.***

$$
\hat{y}_{i} = x_{i}\hat{\beta}
$$

***Where***

$$
\hat{\beta}= \left( \sum_{i=1}^{n}{x_{i}y_{i}}  \right) /
             \left( \sum_{i'=1}^{n}{x_{i'}^2}  \right)
$$

- ***Show that we can write***

$$
\hat{y}_{i} = \sum_{i'=1}^{n}{a_{i'}y_{i'}}
$$ I am not sure about this execise as I don’t understand the difference
between $i$ and $i'$.

$$
\begin{split}
\sum_{i'=1}^{n}{a_{i'}y_{i'}} & = x_{i}\hat{\beta} \\
\sum_{i'=1}^{n}{a_{i'}y_{i'}} & = x_{i}\frac{\sum_{i=1}^{n}{x_{i}y_{i}}}
                                            {\sum_{i'=1}^{n}{x_{i'}^2} } \\
\sum_{i'=1}^{n}{a_{i'}} \sum_{i'=1}^{n}{y_{i'}} & = \frac{x_{i}\sum_{i=1}^{n}{x_{i}}}
                                                         {\sum_{i'=1}^{n}{x_{i'}^2} } 
                                                    \sum_{i=1}^{n} {y_{i}} \\
\sum_{i'=1}^{n}{a_{i'}} & = \frac{x_{i}\sum_{i=1}^{n}{x_{i}}}
                                                         {\sum_{i'=1}^{n}{x_{i'}^2} }
\end{split}
$$

6.  ***Using (3.4), argue that in the case of simple linear regression,
    the least squares line always passes through the point
    $(\overline{x},\overline{x})$.***

As you can see bellow the intercept it’s the responsible for that
property.

$$
\begin{split}
\hat{y} & = \left( \hat{\beta}_{0} \right) + \hat{\beta}_{1} \overline{x} \\
\hat{y} & = \overline{y} - \hat{\beta}_{1}\overline{x} + \hat{\beta}_{1} \overline{x} \\
\hat{y} & = \overline{y}
\end{split}
$$

## Applied

7.  **This question involves the use of simple linear regression on the
    Auto data set.**

- ***Use the lm() function to perform a simple linear regression with
  mpg as the response and horsepower as the predictor. Use the summary()
  function to print the results. Comment on the output.***

``` r
library(ISLR2)

AutoModel1 <- lm(mpg ~ horsepower, data = Auto)

summary(AutoModel1)
```


    Call:
    lm(formula = mpg ~ horsepower, data = Auto)

    Residuals:
         Min       1Q   Median       3Q      Max 
    -13.5710  -3.2592  -0.3435   2.7630  16.9240 

    Coefficients:
                 Estimate Std. Error t value Pr(>|t|)    
    (Intercept) 39.935861   0.717499   55.66   <2e-16 ***
    horsepower  -0.157845   0.006446  -24.49   <2e-16 ***
    ---
    Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

    Residual standard error: 4.906 on 390 degrees of freedom
    Multiple R-squared:  0.6059,    Adjusted R-squared:  0.6049 
    F-statistic: 599.7 on 1 and 390 DF,  p-value: < 2.2e-16

As we see the regression p-value is much lower than 0.05 and we can
reject the null hypotheses to conclude that there is a **strong
relationship** between the response en the predictor. The coefficient of
horsepower is negative, so we know that as the predictor increase the
response decrease.

- ***What is the predicted mpg associated with a horsepower of 98? What
  are the associated 95 % confidence and prediction intervals.***

``` r
predict(AutoModel1, newdata = data.frame(horsepower = 98), interval = "confidence")
```

           fit      lwr      upr
    1 24.46708 23.97308 24.96108

``` r
predict(AutoModel1, newdata = data.frame(horsepower = 98), interval = "prediction")
```

           fit     lwr      upr
    1 24.46708 14.8094 34.12476

- ***Plot the response and the predictor. Use the abline() function to
  display the least squares regression line.***

``` r
plot(Auto$horsepower,Auto$mpg)
abline(AutoModel1)
```

![](03-execises_files/figure-commonmark/unnamed-chunk-3-1.png)

- ***Use the plot() function to produce diagnostic plots of the least
  squares regression fit. Comment on any problems you see with the
  fit.***

``` r
par(mfrow = c(2, 2))
plot(AutoModel1)
```

![](03-execises_files/figure-commonmark/unnamed-chunk-4-1.png)

``` r
par(mfrow = c(1, 1))
```

The *Residuals vs Fitted* shows that the relation is not linear and
variance isn’t constant.

9.  ***This question involves the use of multiple linear regression on
    the Auto data set.***

- ***Produce a scatterplot matrix which includes all of the variables in
  the data set.***

``` r
pairs(Auto)
```

![](03-execises_files/figure-commonmark/unnamed-chunk-5-1.png)