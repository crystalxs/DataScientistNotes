# Using R for Linear Regression

## Load Data into R

1. Load via path of data: `myDataFrame <-read.csv("/Users/crystal/xsun45/data/504/BodyFatPercentage.csv")`
2. Load via select data from computer: `myDataFrame <-read.csv(choose.file())`

## Create Regression Model

### Simple Linear Regression Model

```R
myModel <- lm(BODYFAT~WRIST, data = myDataFrame)
summary(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%289%29.png)

The `Std. Error` is the standard error associated with $$\beta_i$$. The `t value` and `Pr(>|t|)` associated with coefficients are the T test for null hypothesis test, which is $$\beta_i = 0$$.

The `Residual standard error` is the square root of the `MSE`.

The `F-statistic` is the F test for the overall significance of the regression.

#### After we create the linear regression model, we could also plot it with original data set to see the fit.

```R
plot(myDataFrame$WRIST, myDataFrame$BODYFAT, pch = 16, cex = 0.5)
abline(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%282%29.png)

### Multi-linear Regression

```R
myDataFrame <- read.csv("/Users/crystal/xsun45/data/601/KelleyBlueBookData.csv")
myModel <- lm(Price ~ Mileage + as.factor(Type) + as.factor(Cylinder) + Liter + Cruise + Sound + Leather, data = myDataFrame)
summary(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%288%29.png)

### Logistic Regression

```R
myModel <- glm(MYOPIC~as.factor(MOMMY)+as.factor(DADMY)+SPORTHR+READHR+COMPHR+STUDYHR+TVHR+as.factor(GENDER), data = myopia, family = "binomial")
summary(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2812%29.png)

#### Test for null deviance model \(the overall significance of the regression\)

```R
lrtest(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%285%29.png)

```R
1-pchisq(myModel$null.deviance-myModel$deviance, myModel$df.null-myModel$df.residual)
```

#### Pseudo R-squared

```R
efronR = function(x) {
  1 - sum((x$y-x$fitted.values)^2)/sum((x$y-mean(x$y))^2)
}
(pesudoR <- efronR(myModel))

mcFaddenR = function(x) {
   1 - x$deviance/x$null.deviance
}
(pesudoR2 <- mcFaddenR(myModel))
```

```R
DescTools::PseudoR2(myModel, "effron")
DescTools::PseudoR2(myModel, "McFadden")
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2815%29.png)

## Confidence Interval & Hypothesis test

### Get Confidence Interval and Hypothesis test for Coefficients

$$
\frac{b_i-\beta_i}{S(b_i)} \sim t(1-\frac{1-\alpha}{2},n-p)
$$

1. Calculate Confidence Interval by hand: 

   To calculate `t value`:

   ```
   t <- qt(1-(1-0.95)/2, n-p)
   ```

   To get $$S(b_i)$$ from `myModel`: `mySummary$coefficients[i, 2]`

2. Calculate Confidence interval by using built-in function:

   ```
   confint(myModel, level = 0.95)
   ```

3. Do hypothesis test by hand:

   To calculate `p value`:

   ```
   t <- 1 - pt(t, n-p)
   ```

   To calculate `t value` for threshold:

   ```
   t <- qt(1-(1-0.95)/2, n-p)
   ```

### Predict and Confidence Interval for Prediction

1. Predict by using regression model: 

   ```R
   pbodyfat <- predict(myModel, data.frame(WRIST = 60))
   
   # logistic regression model
   pMyopia <- predict(myModel, new, type = c("response"))
   ```

2. Prediction Interval for prediction:

   ```R
   pbodyfat <- predict(myModel, data.frame(WRIST = 60), interval = "prediciton", level = 0.8)
   ```

3. Confidence Interval for prediction:

   ```R
   pbodyfat <- predict(myModel, data.frame(WRIST = 60), interval = "confidence", level = 0.9)
   ```

4. Calculate prediction intervals by hand:

   ```R
   pbodyfat <- predict(myModel, data.frame(WRIST = 60), se.fit = TRUE)
   ```

   This function will output the prediction value and the standard errors associated with it.

### ANOVA table

```R
anova(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2813%29.png)

This anova table doesn't include the information about regression.

### Restricted F test

$$
F = \frac{\frac{SSE_R - SSE_{UR}}{q}}{\frac{SSE_{UR}}{n-p}} \sim F(q, n-p)
$$

```R
# Created a restricted linear regression model
myModelR <- lm(Price ~ Mileage + as.factor(Type) + as.factor(Cylinder) + Cruise + Leather, data = kbbd)

(anova(myModel, myModelR))
```

![](/Users/crystal/temp/.gitbook/assets/image%20%287%29.png)

#### Doing F test by hand

```R
pValue <- 1 - pf(((sseR-sseUR)/q)/(sseUR/(n-p)), q, n-p)
```

## Exam the Data

### Leverage, Outlier, Inflation

```R
rstandard(myModel) #semi-studentized
# studentized/outlier
rstudent(myModel)
studres(myModel)
hatvalues(myModel) # leverage
cooks.distance(myModel) # influence point
influencePlot(myModel)
```



![influence plot](/Users/crystal/temp/.gitbook/assets/image%20%2835%29.png)

### Heteroscedasticity in residuals

#### Breush-Pagan Test

$$
H_0: \gamma_0 = \gamma_1 = \gamma_2 = ... = \gamma_p = 0
$$

```R
lmtest::bptest(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%286%29.png)

#### Residual plots

```R
plot(myModel, pch = 16, cex = 0.5, which = 3)
```

![the square root of the absolute value of the standardized residuals against the fitted values](/Users/crystal/temp/.gitbook/assets/image%20%2824%29.png)

```R
plot(myModel, pch = 16, cex = 0.5, which = 1)
```

![Residual Plot](/Users/crystal/temp/.gitbook/assets/image%20%2843%29.png)

#### Hull-White heteroscedasticity-robust standard errors

```R
myNewVCVMatrix <- vcovHC(myModel, type = "HC1")
coeftest(myModel, myNewVCVMatrix)
coefci(myModel, vcov. = myNewVCVMatrix, level = 0.95)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2837%29.png)

### Serial Correlation

#### The studentized fitted residuals are plotted as a time series

i.e., the x-axis is the index of the position of the case in the data set and the y-axis is value of the associated studentized fitted residual

```R
plot(studres(myModel), pch = 16, cex = 0.5)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2833%29.png)

#### Construct the tuples $$(e_i, e_i+1)$$ and make a scatterplot of them

```R
plot(myModel$residuals[1:29], myModel$residuals[2:30], pch = 16, cex = 0.5)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2828%29.png)

#### Breusch-Godfrey test for serial correlation of residuals

```R
lmtest::bgtest(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2825%29.png)

### Normality

#### P-P plot

```R
CircStats::pp.plot(cakedr$X7.173778602)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2840%29.png)

#### Q-Q plot

```R
plot(myModel, which = 2)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2841%29.png)

#### Jarque-Bera test

```R
jarque.bera.test(myModel$residuals)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2829%29.png)

#### Kolmogorov-Smirnov test

```R
y = rnorm(length(myModel$residuals), mean = 0, sd = sqrt(anova(myModel)[6,3]))
ks.test(myModel$residuals, y)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2821%29.png)

### Omit variable

#### Ramsey RESET test

```R
resettest(myModel, 2:3, type = "regressor")
resettest(myModel, 2:3, type = "fitted    ")
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2831%29.png)

### Multi-collinearity

#### Variance Inflation Factors

```R
vif(myModel)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%284%29.png)

#### Ridge Regression

```r
myRidgeModel <- lm.ridge(calories~sugars+carbo+protein+fat+fiber+vitamins+as.factor(mfr)+as.factor(type)+rating, data = bfc, lambdas = seq(-1,1,0.001))
summary(myRidgeModel)
```

