# Multiple linear regression

Linear regression is useful if only one value can vary.
However in many real world examples multiple values will influence the true out coming value.

Hence it is important to use <strong>multiple linear regression</strong>

It is based on this formula:

<img src="https://miro.medium.com/max/818/1*UG5Tb19HVj__78ifl37P3g.png">


## Review


- it works just as two variable linear regression, just with more variables
- It uses a set of independent variables to learn how to find the optimal parameters (parameters are the m values and the intercept value b)
- The learning process is done by labeled data, and is done after the operator confirms via R<sup>2</sup> (Residual value) value the model precision
- scikit-learn `LinearRegression()` can be used to perform either multiple or single linear regression
- Residual analysis is used to evaluate the model's accuracy (R<sup>2</sup>)
- scikit-learn comes with a `.score(x, y)` methode which returns R<sup>2</sup> 

### Equations

<img src="../pictures/multiple-linear-regression-eq.PNG">