An Introduction to Statistical Learning
================

- <a href="#general-concepts" id="toc-general-concepts"><span
  class="toc-section-number">1</span> General concepts</a>
  - <a href="#reducible-and-irreducible-error"
    id="toc-reducible-and-irreducible-error"><span
    class="toc-section-number">1.1</span> Reducible and irreducible
    error</a>
  - <a href="#types-of-models" id="toc-types-of-models"><span
    class="toc-section-number">1.2</span> Types of models</a>
  - <a href="#evaluating-model-performance"
    id="toc-evaluating-model-performance"><span
    class="toc-section-number">1.3</span> Evaluating model performance</a>
- <a href="#generalized-linear-models-glm"
  id="toc-generalized-linear-models-glm"><span
  class="toc-section-number">2</span> Generalized linear models (GLM)</a>
  - <a href="#linear-regresion" id="toc-linear-regresion"><span
    class="toc-section-number">2.1</span> Linear regresion</a>
    - <a href="#getting-the-least-squares-line-of-a-sample"
      id="toc-getting-the-least-squares-line-of-a-sample"><span
      class="toc-section-number">2.1.1</span> Getting the Least Squares Line
      of a sample</a>
    - <a href="#getting-confident-intervarls-of-coeffients"
      id="toc-getting-confident-intervarls-of-coeffients"><span
      class="toc-section-number">2.1.2</span> Getting confident intervarls of
      coeffients</a>
    - <a href="#insights-to-extract" id="toc-insights-to-extract"><span
      class="toc-section-number">2.1.3</span> Insights to extract</a>
    - <a href="#standard-linear-regression-model-assumptions"
      id="toc-standard-linear-regression-model-assumptions"><span
      class="toc-section-number">2.1.4</span> Standard linear regression model
      assumptions</a>
    - <a href="#possible-problems" id="toc-possible-problems"><span
      class="toc-section-number">2.1.5</span> Possible problems</a>
    - <a href="#avoid-using-for-classification-problems"
      id="toc-avoid-using-for-classification-problems"><span
      class="toc-section-number">2.1.6</span> Avoid using for classification
      problems</a>
  - <a href="#poisson-regression" id="toc-poisson-regression"><span
    class="toc-section-number">2.2</span> Poisson Regression</a>
  - <a href="#logistic-regression" id="toc-logistic-regression"><span
    class="toc-section-number">2.3</span> Logistic Regression</a>
    - <a href="#estimating-coefficients"
      id="toc-estimating-coefficients"><span
      class="toc-section-number">2.3.1</span> Estimating coefficients</a>
    - <a href="#multiple-regression" id="toc-multiple-regression"><span
      class="toc-section-number">2.3.2</span> Multiple regression</a>
    - <a href="#interpreting-the-model" id="toc-interpreting-the-model"><span
      class="toc-section-number">2.3.3</span> Interpreting the model</a>
    - <a href="#multinomial-logistic-regression"
      id="toc-multinomial-logistic-regression"><span
      class="toc-section-number">2.3.4</span> Multinomial Logistic
      Regression</a>
    - <a href="#model-limitatios" id="toc-model-limitatios"><span
      class="toc-section-number">2.3.5</span> Model limitatios</a>
- <a href="#generative-models-for-classi???cation"
  id="toc-generative-models-for-classi???cation"><span
  class="toc-section-number">3</span> Generative Models for
  Classi???cation</a>
  - <a href="#linear-discriminant-analysis-lda"
    id="toc-linear-discriminant-analysis-lda"><span
    class="toc-section-number">3.1</span> Linear Discriminant Analysis
    (LDA)</a>
  - <a href="#quadratic-discriminant-analysis-qda"
    id="toc-quadratic-discriminant-analysis-qda"><span
    class="toc-section-number">3.2</span> Quadratic Discriminant Analysis
    (QDA)</a>
  - <a href="#naive-bayes" id="toc-naive-bayes"><span
    class="toc-section-number">3.3</span> Naive Bayes</a>
- <a href="#non-parametric-methods" id="toc-non-parametric-methods"><span
  class="toc-section-number">4</span> Non-parametric Methods</a>
  - <a href="#k-nearest-neighbors-knn"
    id="toc-k-nearest-neighbors-knn"><span
    class="toc-section-number">4.1</span> K-nearest neighbors (KNN)</a>
    - <a href="#classi???er" id="toc-classi???er"><span
      class="toc-section-number">4.1.1</span> Classi???er</a>
    - <a href="#regression" id="toc-regression"><span
      class="toc-section-number">4.1.2</span> Regression</a>

# General concepts

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

The challenge to achieve that goal it???s that we don???t at the beginning
how much of the error correspond to each type.

$$
\begin{split}
E(Y-\hat{Y})^2 & = E[f(X) + \epsilon - \hat{f}(X)]^2 \\
               & = \underbrace{[f(X)- \hat{f}(X)]^2}_\text{Reducible} +
                   \underbrace{Var(\epsilon)}_\text{Irredicible}
\end{split}
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
> Our challenge lies in ???nding a method for which both the variance and
> the squared bias are low.

</div>

## Types of models

- **Parametric methods**
  1.  Make an assumption about the functional form. For example,
      assuming linearity.
  2.  Estimate a small number parameters based on training data.
  3.  Are easy to interpret.
  4.  Tend to outperform non-parametric approaches when there is a small
      number of observations per predictor.
- **Non-parametric methods**
  1.  Don???t make an assumption about the functional form, to accurately
      ???t a wider range of possible shapes for $f$.
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

- **Test error rate**

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

- **Confusion Matrix**

It contracts the model???s outputs with real values and makes easier to
calculate more metrics to validate the model.

<img src="img/14-confution-matrix.png" data-fig-align="center" />

- Some metrics related with the confussion matrix are:

  - **Sensitivity**: Represents the percentage of **positive** values
    that have been correctly identi???ed $\text{TP}/\text{P}$.
  - **Specificity**: Represents the percentage of **negative** values
    that have been correctly identi???ed $\text{TN}/\text{N}$.

You can more metrics in the next table.

<img src="img/14-confution-matrix-metrics.png"
data-fig-align="center" />

The **ROC *(receiver operating characteristics)* Curve** displays the
two types of errors for all possible thresholds. The **area under the
curve (AUC)** the represent overall performance of a classi???er,
summarized over all possible thresholds and as larger the AUC the better
the classi???er.

<img src="img/15-ROC-curve.png" data-fig-align="center" />

# Generalized linear models (GLM)

## Linear regresion

### Getting the Least Squares Line of a sample

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
\hat{\beta}_{1} = \frac{\Sigma_{i=1}^{n}(x_{i}-\overline{x})(y_{i}-\overline{y})}
                       {\Sigma_{i=1}^{n}(x_{i}-\overline{x})}
, \quad
\hat{\beta}_{0} = \overline{y} - \hat{\beta}_{1}\overline{x}
$$

### Getting confident intervarls of coeffients

To estimate the **population regression line** we can calculate
**con???dence intervals** for sample coefficients, to define a range where
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

1.  Each residual have common variance $\sigma^2$, so the variances of
    the error terms shouldn???t have any relation with the value of the
    response.
2.  Residuals are uncorrelated. For example, if $\epsilon_{i}$ is
    positive, that provides little or no information about the sign of
    $\epsilon_{i+1}$.

If not, we would end underestimating the true standard errors, reducing
the probability a given confident level to contain the true value of the
parameter and underrating the *p-values* associated with the model.

$$
\sigma \approx RSE = \sqrt{\frac{RSS}{(n-p-1)}}
$$

Now we can calculate the **standard error** of each coefficient and
calculate the confident intervals.

$$
SE(\hat{\beta_{0}})^2 = \sigma^2 
                       \left[\frac{1}{n}+
                             \frac{\overline{x}^2}
                                  {\Sigma_{i=1}^{n} (x_{i}-\overline{x})^2} 
                       \right]
$$

$$
SE(\hat{\beta_{1}})^2 = \frac{\sigma^2}
                             {\Sigma_{i=1}^{n} (x_{i} - \overline{x})^2}
$$

$$  
\hat{\beta_{1}} \pm 2 \cdot SE(\hat{\beta_{1}}), \quad \hat{\beta_{0}} \pm 2 \cdot SE(\hat{\beta_{0}})
$$

### Insights to extract

#### Confirm the relationship between the Response and Predictors

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

#### Accuracy of the model (relationship strength)

If we want to know how well the model fits to the data we have two
options:

- **Residual standard error (RSE)**: Even if the model were correct, the
  actual values of $\hat{y}$ would differ from the true regression line
  by approximately *this units*, on average. To get the percentage error
  we can calculate $RSE/\overline{x}$

- **The $R^2$ statistic**: The proportion of variance explained by
  taking as a reference the **total sum of squares (TSS)**.

$$
TSS = \Sigma(y_{i} - \overline{y})^2
$$

$$
R^2 = \frac{TSS - RSS}{TSS}
$$

$$
R^2 = 
\begin{cases}
    Cor(X, Y)^2  & \text{Simple Lineal Regresion} \\
    Cor(Y,\hat{Y})^2 & \text{Multipline Lineal Regresion}
\end{cases}
$$

#### Confirm the relationship between the Response and each predictor

To answer that we can test if a particular subset of q of the
coefficients are zero.

$$
H_{0}: \beta_{p-q+1} = \beta_{p-q+2} = \dots = \beta_{p} = 0
$$

In this case, F-statistic reports the **partial e???ect** of adding a
extra variable to the model (the order matters) to apply a *variable
selection* technique. The classical approach is to:

1.  Fit a model for each variable combination $2^p$.
2.  Select the best model based on *Mallow???s Cp*, *Akaike information
    criterion (AIC)*, *Bayesian information criterion (BIC)*, and
    *adjusted* $R^2$ or plot various model outputs, such as the
    residuals, in order to search for patterns.

But just think that if we have $p = 30$ we will have
$2^{30} = =1,073,741,824\ models$ to fit, that it???s too much. Some
alternative approaches for this task:

- Forward selection
- Backward selection (cannot be used if p \>n)
- Mixed selection

#### Size of association between each predictor and the response.

To check that we need to see the $\hat{\beta}_{j}$ *confident intervals*
as the real $\beta_{j}$ is in that range.

#### Predicting future values

If we want to predict the average response $f(X)$ we can use the
confident intervals, but if we want to predict an individual response
$Y = f(X) + \epsilon$ we need to use prediction intervals as they
account for the uncertainty associated with $\epsilon$, the irreducible
error.

### Standard linear regression model assumptions

- The **additivity assumption** means that the association between a
  predictor $X_{j}$ and the response $Y$ does not depend on the values
  of the other predictors, as it happens when there is a *interaction
  (synergy) effect*

- The **linearity assumption** states that the change in the response Y
  associated with a one-unit change in $X_{j}$ is constant, regardless
  of the value of $X_{j}$.

#### Including an interaction term

This approach relax the *additivity assumption* that models usually
have.

- **2 quantitative variables**

It consist in adding an extra coefficient which multiplies two or more
variables.

$$
\begin{split}
Y & = \beta_{0} + \beta_{1} X_{1} + \beta_{2} X_{2} + \beta_{3} X_{1} X_{2} + \epsilon \\
  & = \beta_{0} + (\beta_{1} + \beta_{3} X_{2}) X_{1} + \beta_{2} X_{2} + \epsilon \\
  & = \beta_{0} + \tilde{\beta}_{1} X_{1} + \beta_{2} X_{2} + \epsilon
\end{split}
$$

After adding the interaction term we could interpret the change as
making one of the original coefficient a function of the another
variable. Now we could say that $\beta_{3}$ *represent **the change
of*** $X_{1}$ ***effectiveness** associated with a one-unit increase in*
$X_{2}$.

It very important that we keep **hierarchical principle**, which states
that if we include an interaction in a model, we should also include the
main effects, even if the p-values associated with their coefficients
are not significant as ***it would alter the meaning of the
interaction***.

- **1 quantitative and 1 qualitative variable**

If $X_{1}$ is quantitative and $X_{2}$ is qualitative:

$$
\hat{Y} = 
\begin{cases}
    (\beta_{0} + \beta_{2}) + (\beta_{1} + \beta_{3})X_{1} & \text{if }X_{2} \text{ is TRUE}\\
    \beta_{0} + \beta_{1}X_{1}                             & \text{if }X_{2} \text{ is FALSE}
\end{cases}
$$

Adding the $\beta_{3}$ interaction allow the line to change the line
slope based on $X_{2}$ and not just a different intercept.

<img src="img/03-factor-interaction.png" data-fig-align="center" />

#### Polynomial regression

This approach relax the *linearity assumption* that models usually have.
It consist in including transformed versions of the predictors.

$$
\begin{split}
Y & = \beta_{0} + \beta_{1} X_{1} + \beta_{2} X_{2} \\
  & = \beta_{0} + \beta_{1} X_{1} + \beta_{2} X_{1}^2 
\end{split}
$$

### Possible problems

#### Non-linearity of the response-predictor relationships

| Detection method                                                                                                                                                                                                  | Solutions                                                                                                                                   |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------------------------------------------------------------------------------------------------------------------------------------------|
| Plot the **residuals versus predicted values** $\hat{y}_{i}$. Ideally, the residual plot will show no discernible pattern. The presence of a pattern may indicate a problem with some aspect of the linear model. | A simple approach is to use non-linear transformations of the predictors, such as $\log{X}$, $\sqrt{X}$, and $X^2$, in the regression model |

<img src="img/04-residuals-predicted-values.png"
data-fig-align="center" />

#### Correlation of error terms

| Detection method                                                                                                                                                                                                                                          | Solutions                                                               |
|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------|
| 1\. Plot the residuals from our model as a function of time or execution order. If the errors are uncorrelated, then there should be no discernible pattern. </br> </br> 2. Check if some observation have been exposed to the same environmental factors | Good experimental design is crucial in order to mitigate these problems |

#### Non-constant variance (heteroscedasticity) of error terms

| Detection method                                              | Solutions                                                                              |
|:--------------------------------------------------------------|:---------------------------------------------------------------------------------------|
| Plot the residual plot en check if you can see a funnel shape | We can transform the response using a concave function such as $\log{Y}$ or $\sqrt{Y}$ |

<img src="img/05-non-constance-variance.png" data-fig-align="center" />

#### Outliers

An outlier is a point for which $y_{i}$ is far from the value predicted
by the model. Sometimes, they have little effect on the least squares
line, but *over estimate the RSE* making bigger p-values of the model
and *under estimate the* $R^2$.

| Detection method                                                                                                                                                              | Solutions                                                                                                                                                         |
|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Plot the **studentized residuals**, computed by dividing each residual $e_{i}$ by its estimated standard error. Then search for points which absolute value is greater than 3 | They can be removed if it has occurred due to an error in data collection. Otherwise, they may indicate a deficiency with the model, such as a missing predictor. |

<img src="img/06-studentized-residuals-plot.png"
data-fig-align="center" />

#### High-leverage points

Observations with **high leverage** have an unusual value for $x_{i}$.
High leverage observations tend to have a sizable impact on the
estimated regression line and any problems with these points may
invalidate the entire fit.

| Detection method                                                                                                                                              | Solutions                                                             |
|:--------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------|
| Compute the leverage statistic. Find an observation with higher value than mean, represented by $(p + 1)/n$. Leverage values are always between $1/n$ and $1$ | Make sure that the value is correct and not a data collection problem |

$$
h_{i} = \frac{1}{n} + 
        \frac{(x_{i} - \overline{x})^2}
              {\Sigma_{i'=1}^n(x_{i'} - \overline{x})^2}
$$

In a *multiple linear regression*, it is possible to have an observation
that is well within the range of each individual predictor???s values, but
that is unusual in terms of the full set of predictors.

<img src="img/07-studentized-residuals-leverage-plot.png"
data-fig-align="center" />

#### Collinearity

**Collinearity** refers to the situation in which two or more predictor
variables are closely related (highly correlated) to one another. It
reduces the accuracy of the estimates of the regression coe???cients and
causes the standard error for $\hat{\beta}_{j}$ to grow. That reduce the
**power of the hypothesis test**,that is, the probability of correctly
detecting a non-zero coe???cient.

Looking at the correlation matrix of the predictors could be usefull,
but it is possible for collinearity to exist between three or more
variables even if no pair of variables has a particularly high
correlation (**multicollinearity**).

| Detection method                                                                                                                                                                                                                                                                                                             | Solutions                                                                                                                                      |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:-----------------------------------------------------------------------------------------------------------------------------------------------|
| The best way to assess multicollinearity is to compute the **variance in???ation factor (VIF)**, which is the ratio of the variance of $\hat{\beta}_{j}$ when ???tting the full model divided by the variance of $\hat{\beta}_{j}$ if ???t on its own with 1 as its lowest value and 5 or 10 as problematic values of collinearity | 1\. Drop one of the problematic variables from the regression. </br> </br> 2. Combine the collinear variables together into a single predictor |

$$
\text{VIF}(\hat{\beta}_{j}) = \frac{1}
                                   {1 - R_{X_{j}|X_{-j}}^2}
$$

Where $R_{X_{j}|X_{-j}}^2$ is the $R^2$ from a regression of $X_{j}$
onto all of the other predictors.

### Avoid using for classification problems

There are better model to achieve that kind of situation. For example,
he linear **discriminant analysis (LDA)** procedure the same response of
a linear regression for a binary problem. Other reasons are:

- A regression method cannot accommodate a qualitative response with
  more than two classes.
- A regression method will not provide meaningful estimates of $Pr(Y|X)$
  as some of our estimates might be outside the \[0, 1\] interval.

## Poisson Regression

If $Y \in \{ 0, 1, 2, 3, \dots \}$ that could be the result after
**counting** a particular event the *linear regression* might not meet
our needs as it could bring negative numbers. The **Poisson
Distribution** follow the next function:

$$
Pr(Y = k) = \frac{e^{-\lambda} \lambda^{k}}
                 {k!}
$$

Where: - $\lambda$ must be greater than 0. It represents the expected
number of events $E(Y)$ and variance related $Var(Y)$ - $k$ represent
the number of events that we want to evaluate base of $\lambda$. Its
numbers should be greater or equal to 0.

So, it makes sense that the value that we want to predict with our
regression would be $\lambda$, by using next structure:

$$
\log{ \left( \lambda(X_1, X_2, \dots , X_p)  \right)} = \beta_0 + \beta_1 X_1 + \dots + \beta_p X_p
$$

If select this model we need to be aware how to interpret the
coefficients. For example, if $\beta_1 = -0.08$ for a categorical
variable, we can conclude by calculating $e^{-0.08}$ that ***92.31%***
of events of the base line related to $\beta_0$ would happen.

## Logistic Regression

It models the **probability** ($p(X) = Pr(Y=1|X)$) that Y belongs to a
particular category given some predictors by assuming that $Y$ follows a
**Bernoulli Distribution**. This model calculates the probability using
the ***logistic function*** which produce a S form between 0 and 1:

$$
p(X) = \frac{e^{\beta_{0}+\beta_{1}X}}
            {1+e^{\beta_{0}+\beta_{1}X}}
$$

<img src="img/09-logistic-function-example.png"
data-fig-align="center" />

As the functions returns probabilities is responsibility of the analyst
to define a **threshold** to make classifications.

### Estimating coefficients

To estimate $\hat{\beta}_{0}$ and $\hat{\beta}_{1}$ the method used is
called as *maximum likelihood* which consists in maximizing the
**likelihood function**. It is important to clarify that the *least
squares approach* is in fact a special case of maximum likelihood.

$$
\ell(\beta_{0}, \beta_{1}) = \prod_{i:y_{i} = 1}p(x_{i})\prod_{i':y_{i'} = 0}p(1-x_{i'})
$$

### Multiple regression

We also can generalize the *logistic function* as you can see bellow.

$$
p(X) = \frac{e^{\beta_{0}+\beta_{1}X_{1}+\dots+\beta_{p}X_{p}}}
            {1+e^{\beta_{0}+\beta_{1}X_{1}+\dots+\beta_{p}X_{p}}}
$$

### Interpreting the model

To understand how each variable influence the probability $p(X)$, we
need to manipulate the *logistic function* until having a lineal
combination on the right site.

$$
\underbrace{ \log{ \left( \overbrace{\frac{p(X)}{1 - p(X)}}^\text{odds ratio} \right)} }_\text{log odds or logit} = \beta_{0}+\beta_{1}X 
$$

As we can see, the result of the linear combination is the $\log$ of the
*odds ratio*, known as **log odd** or **logit**.

An **odds ratio** of an event presents the likelihood that the event
will occur as a proportion of the likelihood that the event won???t occur.
It can take any value between $0$ and $\infty$, where low probabilities
are close to $0$, higher to $\infty$ and equivalents ones are equals
to 1. For example, if we have an $\text{odds ratio} = 2$, we can say
that it???s 2 times more likely that the event happens rather than not.

Applying $\log{(\text{odds ratio})}$ makes easier to compare the effect
of variables as values below 1 become negative numbers of the scale of
possible numbers and 1 becomes 0 for non-significant ones. To have an
idea, an odds ratio of 2 has the same effect as 0.5, which it???s hard to
see at first hand, but if we apply the $\log$ to each value we can see
that $\log{(2)} = 0.69$ and $\log{(0.5)} = -0.69$.

At end, $p(X)$ will increase as $X$ increases if $\beta_{1}$ is positive
despite the relationship between each other isn???t a linear one.

#### Understanding a confounding paradox

| Simple Regression                                                                                                                                          | Multiple Regression                                                                                                                                   |
|:-----------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------------------------------------------------------------------------------------------|
| <img src="img/10-Default-table-4_2.png" data-fig-align="center" />                                                                                         | <img src="img/11-Default-table-4_3.png" data-fig-align="center" />                                                                                    |
| The positive coe???cient for student indicates that for **over all values of balance and income**, a student is *more* likely to default than a non-student. | The negative coe???cient for student indicates that for a **???xed value of balance and income**, a student is less likely to default than a non-student. |

<img src="img/12-Default-multiple-plot-4_3.png"
style="width:60.0%;height:60.0%" data-fig-align="center" />

The problem relays on the fact that *student* and *balance* are
**correlated**. In consequence, a student is riskier than a non-student
if no information about the student???s credit card balance is available.
However, that student is less risky than a non-student with the *same
credit card balance*!

<img src="img/13-Default-simple-plot-4_3.png"
style="width:60.0%;height:60.0%" data-fig-align="center" />

### Multinomial Logistic Regression

We also can generalize the *logistic function* to support more than 2
categories ($K > 2$) by defining by convention the last category $K$ as
a **baseline**.

For $k = 1, \dotsc,K-1$ we use function.

$$
Pr(Y = k|X= x) = \frac{e^{\beta_{k0}+\beta_{k1}x_{1}+\dots+\beta_{kp}x_{p}}}
                      {1+\sum_{l=1}^{K-1}e^{\beta_{l0}+\beta_{l1}x_{1}+\dots+\beta_{lp}x_{p}}}
$$

For $k=K$, we use the function.

$$
Pr(Y = K|X= x) = \frac{1}
                      {1+\sum_{l=1}^{K-1}e^{\beta_{l0}+\beta_{l1}x_{1}+\dots+\beta_{lp}x_{p}}}
$$ And after some manipulations we can show that $\log$ of the
probability of getting $k$ divided by the probability of the *baseline*
is equivalent to a linear combinations of the functions parameters.

$$
\log{ \left( \frac{Pr(Y = k|X= x)}{Pr(Y = K|X= x)} \right)} = \beta_{k0}+\beta_{k1}x_{1}+\dots+\beta_{kp}x_{p}
$$

In consequence, each coefficient represent a measure of how much change
the probability from the baseline probability.

### Model limitatios

There are models that could make better classifications when:

- There is a substantial separation between the $Y$ classes.
- The predictors $X$ are approximately normal in each class and the
  sample size is small.
- When the decision boundary is not lineal.

# Generative Models for Classi???cation

These models instead of trying to predict the **posterior probability**
( $Pr(Y=k|X=x)$ ) directly, they try to estimate the distribution of the
predictors $X$ separately in each of the response classes $Y$ (
$f_{k}(X) = Pr(X|Y=k)$ ). Then, they use the **Bayes??? Theorem** and the
**overall or prior probability** $\pi_{k}$ (probability of a randomly
chosen observation comes from the $k$th class) to flip these around into
estimates for $Pr(Y=k|X=x)$ by approximating the ***Bayes Classifier***,
which has the lowest ***total error rate***.

$$
p_{k}(x) = Pr(Y = k | X = x) = \frac{\pi_{k} f_{k}(x)} {\sum_{l=1}^{K} \pi_{l} f_{l}(x)}
$$

Estimating the *prior probability* can be as easy calculate
$\hat{\pi}_{k} = n_{k}/ n$ for each $Y$ class by assuming that the
trainning data its representative of the population, but estimating the
density function of $X$ for each class $f_{k}$ it???s more challenging, so
models need to make more simplifying assumptions to estimate it.

## Linear Discriminant Analysis (LDA)

This model assumes that:

- The density function of $X$ for each $Y$ class $f_{k}$ follows a
  **Normal (Gaussian) distribution** within each class. Even though, it
  is often remarkably robust to model violations like Boolean variables.
- $X$ has a **different mean** across all $Y$ classes
  $\mu_{1}^2 \neq \dots \neq \mu_{k}^2$.
- $X$ has a **common variance** across all $Y$ classes
  $\sigma_{1}^2 = \dots = \sigma_{k}^2$.

To understand how the model calculates its parameters, let???s see the
**discriminant function** when the number of predictors is $p=1$ and the
number of $Y$ classes is $K=2$.

$$
\begin{split}
\delta_{k}(x) & = \log{ \left( p_{x}(x) \right)} \\ 
              & = \log{(\pi_{k})} 
                - \frac{\mu_{k}^2}{2\sigma^2} 
                + x \cdot \frac{\mu_{k}}{\sigma^2} 
\end{split}
$$

In this function, it???s clear that a class $k$ has more possibilities to
be selected as mean of $x$ for that particular class increases and its
variance decreases. It is also important to take in consideration the
effect of $\log{(\pi_{k})}$, in consequence the proportion of classes
also influence the results.

If we want to extend the model to work with $p \geq 1$ we also need to
consider that:

- Each individual predictor follows a one-dimensional normal
  distribution
- There is some correlation between each pair of predictors

As result, the *discriminant function* is:

$$
\begin{split}
\delta_{k}(x) & = \log{\pi_{k}}  - \frac{1}{2} \mu_{k}^T \Sigma^{-1} \mu_{k} \\
                & \quad + x^T \Sigma^{-1} \mu_{k}
\end{split}                      
$$

- Where:

  - $x$ refers to a vector the current value of each $p$ element.
  - $\mu$ refers to a vector with the mean of each predictor.
  - $\Sigma$ refers to the covariance matrix $p \times p$ of
    $\text{Cov}(X)$.

The model also can be extended to handle $K > 2$ after defining the $K$
class as the baseline, we can extend the *discriminant function* to have
the next form:

$$
\begin{split}
\delta_{k}(x) & = \log{ \left( 
                        \frac{Pr(Y = k|K=x)}
                             {Pr(Y=K|X=x)}
                      \right)} \\
              & = \log{ \left( \frac{\pi_{k}}{\pi_{K}} \right)}
                  - \frac{1}{2} (\mu_{k} + \mu_{K})^T \Sigma^{-1} (\mu_{k} - \mu_{K}) \\
              & \quad + x^{T} \Sigma^{-1} (\mu_{k} - \mu_{K})
\end{split}
$$

## Quadratic Discriminant Analysis (QDA)

Like LDA, the QDA classi???er plugs estimates for the parameters into
Bayes??? theorem in order to perform prediction results and assumes that:

- The observations from each class are drawn from a Gaussian
  distribution
- Each class has its own **covariance matrix**,
  $X \sim N(\mu_{k}, \Sigma_{k})$

Under this assumption, the Bayes classi???er assigns an observation
$X = x$ to the class for which $\delta_{k}(x)$ is largest.

$$
\begin{split}
\delta_{k}(x) = & \quad \log{\pi_{k}} 
                - \frac{1}{2} \log{|\Sigma_{k}|} 
                - \frac{1}{2} \mu_{k}^T \Sigma_{k}^{-1}\mu_{k} \\
              & + x^T \Sigma_{k}^{-1} \mu_{k} \\
              & - \frac{1}{2} x^T \Sigma_{k}^{-1} x
\end{split}                  
$$

In consequence, QDA is more flexible than LDA and has the potential to
be more accurate in settings where interactions among the predictors are
important in discriminating between classes or when we need non-linear
decision boundaries.

The model also can be extended to handle $K > 2$ after defining the $K$
class as the baseline, we can extend the *discriminant function* to have
the next form:

$$
\log{ \left( \frac{Pr(Y = k|K=x)}{Pr(Y=K|X=x)} \right)} = 
a_k + \sum_{j=1}^{p}b_{kj}x_{j} + 
      \sum_{j=1}^{p} \sum_{l=1}^{p} c_{kjl} x_{j}x_{l}
$$

Where $a_k$, $b_{kj}$ and $c_{kjl}$ are functions of $\pi_{k}$,
$\pi_{K}$, $\mu_{k}$, $\mu_{K}$, $\Sigma_{k}$ and $\Sigma_{K}$

## Naive Bayes

To estimate $f_{k}(X)$ this model assumes that *Within the kth class,
the p predictors are independent* (correlation = 0) and as consequence:

$$
f_{k}(x) = f_{k1}(x_{1}) \times f_{k2}(x_{2}) \times \dots \times f_{kp}(x_{p})
$$

Even thought the assumption might not be true, the model often leads to
pretty decent results, especially in settings where $n$ is not large
enough relative to $p$ for us to e???ectively estimate the joint
distribution of the predictors within each class.

To estimate the one-dimensional density function $f_{kj}$ using training
data we have the following options:

- We can assume that $X_{j}|Y = k \sim N(\mu_{jk}, \sigma_{jk}^2)$
- We can estimate the distribution by defining bins and creating a
  histogram
- We can estimate the distribution by use a kernel density estimator
- If $X_{j}$ is **qualitative**, we can count the proportion of training
  observations for the $j$th predictor corresponding to each class.

The model also can be extended to handle $K > 2$ after defining the $K$
class as the baseline, we can extend the function to have the next form:

$$
\log{ \left( \frac{Pr(Y = k|K=x)}{Pr(Y=K|X=x)} \right)} = 
\log{ \left( 
        \frac{\pi_{k}}
             {\pi_{K}}
      \right)} 
+
\log{ \left( 
        \frac{\prod_{j=1}^{p} f_{kj}(x_{j}) }
             {\prod_{j=1}^{p} f_{Kj}(x_{j}) }
      \right)}
$$

# Non-parametric Methods

## K-nearest neighbors (KNN)

This method performs worst than a parametric as we starting adding
*noise* predictors. In fact, we will get in the situation where for a
given observation has no *nearby neighbors*, known as **curse of
dimensionality** and leading to a very poor prediction of $f(x_{0})$.

KNN unlike parametric models does not tell us which predictors are
important, making it hard to make inferences using this model.

It also sensible the scale of the variables. Variables that are on a
large scale will have a much larger e???ect on the distance between the
observations, and hence on the KNN classi???er, than variables that are on
a small scale. To solve that problem we can *standardize* the data so
that all variables are given a mean of zero and a standard deviation of
one with the function `scale()`.

### Classi???er

The next function estimates the conditional probability for class $j$ as
the fraction of points in $N_{0}$ whose response values equal $j$.

$$
\text{Pr}(Y = j|X = x_{0}) = \frac{1}{K} 
                      \displaystyle\sum_{i \in N_{0}} I(y_{i} = j)
$$

- Where
  - $j$ response value to test
  - $x_{0}$ is the test observation
  - $K$ the number of points in the training data that are closest to
    $x_{0}$ and reduce the model flexibility
  - $N_{0}$ points in the training data that are closest to $x_{0}$

Then KNN classi???es the test observation $x_{0}$ to the class with the
largest probability.

<img src="img/08-knn-classifier.png" data-fig-align="center" />

### Regression

KNN regression estimates $f(x_{0})$ using the average of all the
training responses in $N_{0}$.

$$
\hat{f}(x_{0}) = \frac{1}{K} 
                      \displaystyle\sum_{i \in N_{0}} y_{i}
$$

- Where
  - $x_{0}$ is the test observation
  - $K$ the number of points in the training data that are closest to
    $x_{0}$ and reduce the model flexibility
  - $N_{0}$ points in the training data that are closest to $x_{0}$
