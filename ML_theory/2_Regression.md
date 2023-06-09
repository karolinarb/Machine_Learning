Regression models (both linear and non-linear) are used for predicting a real value. 
If your independent variable is time, then you are forecasting future values, otherwise your model is predicting present but unknown values. 

For simple, multiple and polynomial linear regression: Don't need to apply feature scaling. In the equation, there is a coefficient next to each independent variable, so it doesn't matter some features have higher values than others.


Machine Learning Regression models:
### - Simple Linear Regression
**$y = b_0 + b_1x_1$**
- Training the Simple Linear Regression model on the Training set
```python
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, y_train)
```
- Predicting the Test set results
 ```python
 y_pred = regressor.predict(X_test)
 ```
 - Visualising
```python
plt.scatter(X_train,y_train, color='red')
plt.plot(X_train, regressor.predict(X_train),color='blue')
plt.title('Salary vs Experience (training set)')
plt.xlabel('Years of experience')
plt.ylabel('salary')
```
```python
plt.scatter(X_test,y_test, color='red')
plt.plot(X_train, regressor.predict(X_train),color='blue')
plt.title('Salary vs Experience (training set)')
plt.xlabel('Years of experience')
plt.ylabel('salary')
```
- Get the equation
```python
print(regressor.coef_)
print(regressor.intercept_)
```

The ordinary least squares (OLS) method can be defined as a linear regression technique that is used to estimate the unknown         parameters in a model. The method relies on minimizing the sum of squared residuals between the actual (observed values of the        dependent variable) and predicted values from the model.

### - Multiple Linear Regression
**$y = b_0 + b_1x_1 + b_2x_2 + ... + b_nx_n$**

Backward Elimination is irrelevant in Python, because the Scikit-Learn library automatically takes care of selecting the statistically significant features when training the model to make accurate predictions.

```python
from sklearn.linear_model import LinearRegression
regressor = LinearRegression()
regressor.fit(X_train, y_train)
```
```python
y_pred = regressor.predict(X_test)
np.set_printoptions(precision=2)
print(np.concatenate((y_pred.reshape(len(y_pred),1), y_test.reshape(len(y_test),1)),axis=1))
```

### - Polynomial Linear Regression
**$y = b_0 + b_1x_1 +b_2(x_1)^2 + ... + b_n(x_1)^n$**


#### Training the polynomial regression model on the whole set
```python
from sklearn.preprocessing import PolynomialFeatures
poly_reg = PolynomialFeatures(degree = 4)
X_poly = poly_reg.fit_transform(X)
lin_reg_2 = LinearRegression()
lin_reg_2.fit(X_poly, y)
```
```python
plt.scatter(X, y, color = 'red')
plt.plot(X, lin_reg_2.predict(poly_reg.fit_transform(X)), color = 'blue')
```

### - Support Vector for Regression (SVR)

```python
from sklearn.svm import SVR
regressor = SVR(kernel = 'rbf')
regressor.fit(X, y)
```
#### Predict a new result: input a scaled value of x and reverse scale to get an actual y value
```python
sc_y.inverse_transform(regressor.predict(sc_X.transform([[6.5]])).reshape(-1,1))
```
### - Decision Tree Regression
```python
from sklearn.tree import DecisionTreeRegressor
regressor = DecisionTreeRegressor(random_state = 0)
regressor.fit(X, y)
```

### - Random Forest Regression
```python
from sklearn.ensemble import RandomForestRegressor
regressor = RandomForestRegressor(n_estimators = 10, random_state = 0)
regressor.fit(X, y)
```

## Evaluating Regression Models Performance
### R squared

- $SS_{res} = SUM (y_i - y_î)^2$
- $SS_{tot} = SUM (y_i - y_{avg})^2$

- $R^2 = 1 - \frac{SS_{res}}{SS_{tot}}$

Rule of thumb - highly dependent on the context!:
- 1.0: perfect fit
- ~0.9: very good
- <0.7: not great
- <0.4: terrible
- <0 : model makes no sense for the data set

### Adjusted R squared

$R^2 = 1 - (1 - R^2) * \frac{n-1}{n-k-1}$
where k = number of independent variables and n = sample size

```python
from sklearn.metrics import r2_score
r2_score(y_test, y_pred)
```
