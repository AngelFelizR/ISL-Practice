An Introduction to Statistical Learning
================

- <a href="#basic-concepts" id="toc-basic-concepts"><span
  class="toc-section-number">1</span> Basic concepts</a>
  - <a href="#reducible-and-irreducible-error"
    id="toc-reducible-and-irreducible-error"><span
    class="toc-section-number">1.1</span> Reducible and irreducible
    error</a>
  - <a href="#types-of-models" id="toc-types-of-models"><span
    class="toc-section-number">1.2</span> Types of models</a>
  - <a href="#evaluating-model-performance"
    id="toc-evaluating-model-performance"><span
    class="toc-section-number">1.3</span> Evaluating model performance</a>
- <a href="#linear-regresion" id="toc-linear-regresion"><span
  class="toc-section-number">2</span> Linear regresion</a>
  - <a href="#getting-the-least-squares-line-of-a-sample"
    id="toc-getting-the-least-squares-line-of-a-sample"><span
    class="toc-section-number">2.1</span> Getting the Least Squares Line of
    a sample</a>
  - <a href="#getting-confident-intervarls-of-coeffients"
    id="toc-getting-confident-intervarls-of-coeffients"><span
    class="toc-section-number">2.2</span> Getting confident intervarls of
    coeffients</a>
  - <a href="#accuracy-of-the-model" id="toc-accuracy-of-the-model"><span
    class="toc-section-number">2.3</span> Accuracy of the Model</a>
  - <a href="#insights-to-extract" id="toc-insights-to-extract"><span
    class="toc-section-number">2.4</span> Insights to extract</a>

# Basic concepts

## Reducible and irreducible error

The goal when we are analyzing data is to find a function that based on
some Predictors and some random noise could explain the Response
variable.

$$
Y = f(X) + \epsilon
$$

**$\epsilon$** represent the **random error** and correspond to the
**irreducible error** as it cannot be predicted using the Predictors in
regression models. It would have a mean of 0 unless are missing some
relevant Predictors.

In classification models, the **irreducible error** is represented by
the **Bayes Error Rate**.

$$
1 -  E\left( 
     \underset{j}{max}Pr(Y = j|X)
     \right)
$$

An error is **reducible** if we can improve the accuracy of $\hat{f}$ by
using a most appropriate statistical learning technique to estimate $f$.

The challenge to achieve that goal it’s that we don’t at the beginning
how much of the error correspond to each type.

$$
E(Y-\hat{Y})^2 = E[f(X) + \epsilon - \hat{f}(X)]^2 \\
= \underbrace{[f(X)- \hat{f}(x)]^2}_\text{Reducible} + 
  \underbrace{Var(\epsilon)}_\text{Irredicible}
$$

The reducible error can be also spitted in two parts:

- **Variance** refers to the amount by which $\hat{f}$ would change if
  we estimate it using a different **training data set**. If a method
  has high variance then small changes in the training data can result
  in large changes of $\hat{f}$.

- **Squared bias** refers to the error that is introduced by
  approximating a real-life problem, which may be extremely complicated,
  by a much simpler model as for example a linear model.

$$
E(y_{0} - \hat{f}(x_{0}))^2 = 
Var(\hat{f}(x_{0})) + 
[Bias(\hat{f}(x_{0}))]^2 + 
Var(\epsilon)
$$

<div>

> **Note**
>
> Our challenge lies in ﬁnding a method for which both the variance and
> the squared bias are low.

</div>

## Types of models

- **Parametric methods**
  1.  Make an assumption about the functional form. For example,
      assuming linearity.
  2.  Estimate a small number parameters based on training data.
  3.  Are easy to interpret.
- **Non-parametric methods**
  1.  Don’t make an assumption about the functional form, to accurately
      ﬁt a wider range of possible shapes for $f$.
  2.  Need a large number of observations in order to obtain an accurate
      estimate for $f$.
  3.  The data analyst must select a level of smoothness (degrees of
      freedom).

<img src="img/01-accuracy-vs-interpretability.png"
data-fig-align="center" />

## Evaluating model performance

To evaluate how good works a models we need to split the available data
in two parts.

- **Training data**: Used to fit the model.
- **Test data**: Used to confirm how well the model works with new data.

Some measurements to evaluate our test data are:

- **Test mean squared error (MSE)**

$$
Ave(y_{0}-\hat{f}(x_{0}))^2
$$

- **Test Error rate**

$$
I(y_{0} \neq \hat{y}_{0}) = 
\begin{cases}
    1 & \text{If } y_{0} \neq \hat{y}_{0} \\
    0 & \text{If } y_{0} = \hat{y}_{0}
\end{cases}
$$

$$
Ave(I(y_{0} \neq \hat{y}_{0}))
$$

# Linear regresion

## Getting the Least Squares Line of a sample

As the *population regression line* is unobserved the *least squares
line* of a sample is a good estimation. To get it we need to follow the
next steps:

1.  Define the function to fit.

$$
\hat{y} = \hat{\beta}_{0} + \hat{\beta}_{1} x
$$

2.  Define how to calculate **residuals**.

$$
e_{i} = y_{i} - \hat{y}_{i}
$$

3.  Define the **residual sum of squares (RSS)**.

$$
RSS = e_{1}^2 + e_{2}^2 + \dots + e_{n}^2
$$

4.  Use calculus or make estimation with a computer to find the
    coefficients that minimize the RSS.

$$
\hat{\beta}_{1} = \frac{\sum_{i=1}^{n}(x_{i}-\overline{x})(y_{i}-\overline{y})}
                       {\sum_{i=1}^{n}(x_{i}-\overline{x})}
, \quad
\hat{\beta}_{0} = \overline{y} - \hat{\beta}_{1}\overline{x}
$$

## Getting confident intervarls of coeffients

To estimate the **population regression line** we can calculate
**conﬁdence intervals** for sample coefficients, to define a range where
we can find the population values with a defined **confidence level**.

> If we want to use 95% of confidence we need to know that after taking
> many samples only 95% of the intervals produced with this **confident
> level** would have the true value (parameter).

To generate confident intervals we would need to calculate the variance
of the *random error*.

$$
\sigma^2 = Var(\epsilon)
$$

But as we can not calculate that variance an alternative can be to
estimate it based on residuals if they meet the next conditions:

1.  Each residual have common variance $\sigma^2$.
2.  Residuals are uncorrelated.

$$
\sigma \approx RSE = \sqrt{\frac{RSS}{(n-p-1)}}
$$

In the next chart we can see how residuals are bigger as the TV budget
increases. So the regression doesn’t meet the second condition, but we
can use bootstrap as an alternative way to calculate confident
intervals.

<img src="img/02-residuals-sales-tv.png" data-fig-align="center" />

Now we can calculate the **standard error** of each coefficient and
calculate the confident intervals.

$$
SE(\hat{\beta_{0}})^2 = \sigma^2 
                       \left[\frac{1}{n}+
                             \frac{\overline{x}^2}
                                  {\sum_{i=1}^{n} (x_{i}-\overline{x})^2} 
                       \right]
$$

$$
SE(\hat{\beta_{1}})^2 = \frac{\sigma^2}
                             {\sum_{i=1}^{n} (x_{i} - \overline{x})^2}
$$

$$  
\hat{\beta_{1}} \pm 2 \cdot SE(\hat{\beta_{1}}), \quad \hat{\beta_{0}} \pm 2 \cdot SE(\hat{\beta_{0}})
$$

## Accuracy of the Model

If we want to know how well the model fits to the data we have two
options:

- **Residual standard error (RSE)**: Even if the model were correct, the
  actual values of $\hat{y}$ would differ from the true regression line
  by approximately *this units*, on average.

- **The $R^2$ statistic**: The proportion of variance explained by
  taking as a reference the **total sum of squares (TSS)**.

$$
TSS = \sum(y_{i} - \overline{y})^2 , \quad R^2 = \frac{TSS - RSS}{TSS}
$$

$$
R^2 = 
\begin{cases}
    Cor(X, Y)^2  & \text{Simple Lineal Regresion} \\
    Cor(Y,\hat{Y})^2 & \text{Multipline Lineal Regresion}
\end{cases}
$$

## Insights to extract

**1. Is there a relationship between the Response and Predictors?**

Use the regression **overall P-value** (based on the F-statistic) to
confirm that at **least one predictor** is related with the Response and
avoid interpretative problems associated with the number of observations
(*n*) or predictors (*p*).

$$
H_{0}: \beta_{1} = \beta_{2} = \dots = \beta_{p} = 0
$$

$$
H_{a}: \text{at least one } \beta_{j} \text{ is non-zero}
$$

**2. Which Predictors are related with the Response?**

To answer that we can test if a particular subset of q of the
cofficients are zero.

$$
H_{0}: \beta_{p-q+1} = \beta_{p-q+2} = \dots = \beta_{p} = 0
$$

In this case, F-statistic reports the **partial eﬀect** of adding a
extra variable to the model (the order matters) to apply a *variable
selection* technique. The classical approach is to:

1.  Fit a model for each variable combination $2^p$.
2.  Select the best model based on *Mallow’s Cp*, *Akaike information
    criterion (AIC)*, *Bayesian information criterion (BIC)*, and
    *adjusted* $R^2$ or plot various model outputs, such as the
    residuals, in order to search for patterns.

But just think that if we have $p = 30$ we will have
$2^{30} = =1,073,741,824\ models$ to fit, that it’s too much. Some
alternative approaches for this task:

- Forward selection
- Backward selection (cannot be used if p \>n)
- Mixed selection

**3. How well does the model ﬁt the data?**

To achieve this we can use **residual standard error**, the **$R^2$**
and **plotting** the data.

**4. How accurate is our prediction?**

We use prediction intervals to answer this question. Prediction
intervals are always wider than conﬁdence intervals, because they
incorporate both the error in the estimate for $f(x)$ (the reducible
error) and the uncertainty as to how much an individual point will diﬀer
from the population regression plane (the irreducible error).
