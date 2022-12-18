02-execises
================

- <a href="#conceptual" id="toc-conceptual"><span
  class="toc-section-number">1</span> Conceptual</a>

## Conceptual

1.  **For each of parts (a) through (d), indicate whether we would
    generally expect the performance of a ﬂexible statistical learning
    method to be better or worse than an inﬂexible method. Justify your
    answer.**

- **The sample size n is extremely large, and the number of predictors p
  is small.**

Better, flexible models reduce bias and quit the variance low when
having a large n.

- **The number of predictors p is extremely large, and the number of
  observations n is small.**

Worse, a flexible model could increase its variance very high when
having small n.

- **The relationship between the predictors and response is highly
  non-linear.**

Better, a lineal model would have a very high bias in this case.

- **The variance of the error terms, i.e. σ2 = Var(ϵ), is extremely
  high.**

Worse, a flexible model would over-fit trying to follow the irreducible
error.

2.  **Explain whether each scenario is a classiﬁcation or regression
    problem, and indicate whether we are most interested in inference or
    prediction. Finally, provide n and p.**

- **We collect a set of data on the top 500 ﬁrms in the US. For each ﬁrm
  we record proﬁt, number of employees, industry and the CEO salary. We
  are interested in understanding which factors aﬀect CEO salary.**

Regression, inference, 500, 4

- **We are considering launching a new product and wish to know whether
  it will be a success or a failure. We collect data on 20 similar
  products that were previously launched. For each product we have
  recorded whether it was a success or failure, price charged for the
  product, marketing budget, competition price, and ten other
  variables.**

Classification, prediction, 20, 14

- **We are interested in predicting the % change in the USD/Euro
  exchange rate in relation to the weekly changes in the world stock
  markets. Hence we collect weekly data for all of 2012. For each week
  we record the % change in the USD/Euro, the % change in the US market,
  the % change in the British market, and the % change in the German
  market.**

Regression, prediction, 52, 4

3.  **We now revisit the bias-variance decomposition.**

- **Provide a sketch of typical (squared) bias, variance, training
  error, test error, and Bayes (or irreducible) error curves, on a
  single plot, as we go from less ﬂexible statistical learning methods
  towards more ﬂexible approaches. The x-axis should represent the
  amount of ﬂexibility in the method, and the y-axis should represent
  the values for each curve. There should be ﬁve curves. Make sure to
  label each one.**

<img src="01-sketch.png" width="400" height="350" />

- **Explain why each of the ﬁve curves has the shape displayed in part
  (a).**

In the example f isn’t lineal, so the the **test error** lower as we add
flexibility until the point the models starts to overfit. The **training
error** always goes down as we increase the flexibility. As we make the
model more flexible **variance** always increase as the model is more
likely to change as we change the training data and the **bias** always
goes down as a more flexible model has fewer assumptions. The **Bayes
error** is the irreducible error we can not change it.

4.  **You will now think of some real-life applications for statistical
    learning.**

- **Describe three real-life applications in which classiﬁcation might
  be useful. Describe the response, as well as the predictors. Is the
  goal of each application inference or prediction? Explain your
  answer.**

|   Goal    | Response                      | Predictors                                                                                                                                                                                          |
|:---------:|:------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Inference | Customer Tower Churn (0 or 1) | Annual Rent, Tower Lat, Tower Log, Tower Type, Number of sites around 10 km, Population around 10 km, Average Annual Salary in the city, contract Rent increases, customer technology               |
| Inference | Employee Churn (0 or 1)       | Months in company, Salary, Number of positions, Major, Sex, Total Salary Change, Bono, Wellness Expend, Number of depends, Home location                                                            |
| Inference | Absent (0 or 1)               | Salary, Rain?, Holiday?, Number of uniforms, distance from home to work place, Months in company, Neighborhood median Salary, number of depends, number of marriage, Work start, Work End, Free day |

- **Describe three real-life applications in which regression might be
  useful. Describe the response, as well as the predictors. Is the goal
  of each application inference or prediction? Explain your answer.**

|   Goal    | Response            | Predictors                                                                                                                   |
|:---------:|:--------------------|:-----------------------------------------------------------------------------------------------------------------------------|
| Inference | Number of likes     | Words, Has a video?, Has a picture?, Post time, hashtag used                                                                 |
| Inference | Velocidad de picheo | Edad, Altura, Peso, Horas de corrida, Cantidad de sentadillas, cantidad de practicas por semana, Años practicando el deporte |
|           |                     |                                                                                                                              |

- **Describe three real-life applications in which cluster analysis
  might be useful.**

|                                Goal                                | Predictors                                                                                                                                           |
|:------------------------------------------------------------------:|------------------------------------------------------------------------------------------------------------------------------------------------------|
|              Classify costumer to improve advertising              | Words searched, products clicked, Explored image, Seconds spent on each product, start time, end time, customer location                             |
|        Classify company towers to see patterns in customers        | Tower Lat, Tower Log, Tower Type, Number of sites around 10 km, Population around 10 km, Average Annual Salary in the city, BTS?, start date, Height |
| Classify football players check which players have similar results | Number of passes on each game, Number of meters run on each game, Position Played, Number of goals, Number of stolen balls, total time played        |
