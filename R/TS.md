# Using R for time series

## First look at data

### Load data and check data

Under R, there is a `Time-Series` object type.

#### Load built-in time-series data

```R
data(AirPassengers)
AirPassengers
```

![timeSeriesObjectType](/Users/crystal/gitbook/image/timeSeriesObjectType.png)

`AirPassenger` is a `Time-Series` data. 

#### Convert data into time series data

```R
elec <- read.csv('/Users/crystal/xsun45/data/604/electronics.csv', header = F)
elec <- ts(elec, start = 1996, frequency = 12)
```

### Time series plot

```R
plot(AirPassengers)
# add some vertical line to check it seasonality
abline(v = seq(1949, 1960, 1), col = "red", lty = 2)
```

![img](plot_zoom_png?width=574&height=610)

## Modeling

### Prepare

```R
# Extracting time as the explanatory variate from the time series framework of data
t <- time(AirPassengers)

# Introducing month as the season
cycle(AirPassengers)

# Introducing month as the season
month <- as.factor(cycle(AirPassengers))
```

### Model the trend-only

#### Linear trend

```R
reg0 <- lm(log(AirPassengers)~t)              # Just model linear trend
summary(reg0)
plot(log(AirPassengers))
points(t,predict.lm(reg0),type='l',col='red') # superimpose the fit of model reg0 on the plot of the data
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2830%29.png)

#### p-order trend

```R
p <- 14
reg0 <- lm(as.numeric(elec) ~ poly(as.numeric(t), degree = p))
summary(reg0)
plot(elec, main = "Number of electronics orders in the Eurozone", ylab = "Number of elecronics orders", xlab = "Year")
points(t,predict.lm(reg0),type='l',col='red')
legend("topleft", 
  legend = c("Observed", "Trend"), 
  col = c("black", "red"),
  lty = c(1, 1))
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2827%29.png)

### Model the seasonal-only

```R
reg1 <- lm(log(AirPassengers)~month)          # Just model seasonal effect
summary(reg1)
plot(log(AirPassengers))
points(t,predict.lm(reg1),type='l',col='red') # superimpose the fit of model reg0 on the plot of the data
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2820%29.png)

### Model with trend and seasonal

```R
reg2 <- lm(log(AirPassengers)~t+month)        # Fitting the model reg2 with linear trend and seasonal effect
summary(reg2)
plot(log(AirPassengers))
points(t,predict.lm(reg2),type='l',col='red') # superimpose the fit of model reg2 on the plot of the data
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2817%29.png)

### Diagnostic plots

```R
par(mfrow=c(2,2))                      # Dividing the plotting page into 4 panels
plot(reg2$fitted, reg2$residuals, main = "Residuals vs. Fitted Values", ylab = "Residuals", xlab = "Fitted Values") # plot of fitted values vs residuals
abline(h = 0, col = "red", lwd = 2)
qqnorm(reg2$residuals) #qq-plot of residuals
qqline(reg2$residuals, col = "red")    # plotting the line, along which the dots in qq-plot should lie
plot(reg2$residuals, main = "Residuals vs. Time", ylab = "Residuals", xlab = "Time") # plotting the residuals vs time
abline(h = 0, col = "red", lwd = 2)    # plotting a horizontal line at 0
acf(reg2$residuals, main = "ACF Plot of Residuals") #sample acf plot of residuals
```

![img](http://127.0.0.1:38247/graphics/plot_zoom_png?width=574&height=610)

The **residuals vs. fitted values** plot indicates a fairly **random** scattering of points; there are no obvious "**funnel-shaped**" trends suggesting that the **error variance is indeed constant**.

The **QQ-plot** indicates that the residual quantiles match fairly closely with the theoretical Normal quantiles (**straight line**), suggesting that the **Normality assumption** is reasonable.

The **residuals vs. time** oder also suggests that the error varianes \( $$\sigma^2$$\) does not depend much on time, suggesting that the **constant variance assumption** is reasonable.

The **ACF plot** indicates significant autocorrelation at lags 1 to 14, suggesting that residuals separated in time by 1 to 12 time points are significantly correlated, which contradicts the assumption that the **errors are independent**.

### Prediction

```R
t.new <- seq(1961,1963,length=25)[1:24]  # Intoducing new time for forecatsting 2 years 1961 and 1962 (notice that it is 1:24 because 1963 should not be included)
t2.new <- t.new^2
month.new <- factor(rep(1:12,2))         # Introducing the seasonal value for forecasting

new <- data.frame(t=t.new, t2=t2.new, month=month.new) # Putting the values for forecasting into a dataframe
pred <- predict.lm(reg4,new,interval='prediction')     # Computing the prediction as well as prediction interval

par(mfrow=c(1,1))
plot(AirPassengers,xlim=c(1949,1963),ylim=c(0,900))    #plotting the data

abline(v=1961,col='blue',lty=2)          # adding a vertical line at the point where prediction starts
lines(exp(pred[,1])~t.new,type='l',col='red')          # plotting the predict
lines(exp(pred[,2])~t.new,col='green')   # plotting lower limit of the prediction interval
lines(exp(pred[,3])~t.new,col='green')   # plotting upper limit of the  prediction interval
```

![Rplot](/Users/crystal/gitbook/image/Rplot.png)

## Sample ACF

#### Sample ACF for IID noise N\(0,1\)

```text
X <- rnorm(100)                   # generating (independently) 100 realizations of N(0,1)
par(mfrow=c(2,1))                 #dividing the page into 2 rows and one column
plot(X,type='l',main='iid noise') #plotting the data
acf(X,main='Sample ACF for iid noise', lag.max = 100) # plotting the acf
```

![](/Users/crystal/temp/.gitbook/assets/image%20%283%29.png)

#### Sample ACF for MA\(1\) process

```text
X <- arima.sim(list(order = c(0,0,1), ma = 0.85), n = 200) # simulating data from an MA(1) process
par(mfrow=c(2,1)) #dividing the page into 2 rows and one column
plot(X,type='l',main='Simulated data from MA(1)') #plotting the data
acf(X,main='Sample ACF for MA(1)') # plotting the acf
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2842%29.png)

```text
arima(x=X, order = c(0,0,1))
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2811%29.png)

#### Sample ACF for AR\(1\) process

```text
X <- arima.sim(list(order = c(1,0,0), ar = .7), n = 10000) # simulating data from an AR(1) process
par(mfrow=c(2,1)) #dividing the page into 2 rows and one column
plot(X,type='l',main='Simulated data from AR(1)') #plotting the data
acf(X,main='Sample ACF for AR(1)', lag.max = 120) # plotting the acf
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2819%29.png)

```text
arima(X,order=c(1,0,0))
arima(X,order=c(2,0,0))
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2834%29.png)

#### Sample ACF for data with trend

```text
a <- seq(1,100,length=200)
X <- 22-15*a+0.3*a^2+rnorm(200,500,50)
par(mfrow=c(2,1)) #dividing the page into 2 rows and one column
ts.plot(X, main = "Time Series With Significant Trend")
acf(X, main = "ACF Exhibits Seasonality + Slow Decay", lag.max = 60)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2814%29.png)

#### Sample ACF for data with seasonality

```text
X <- 100*sin(1:200)+rnorm(200, 0, 0.5) 
par(mfrow=c(2,1))
ts.plot(X, main = "Time Series With Significant Seasonality")
acf(X, main = "ACF Also Exhibits Seasonality", lag.max=60)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2826%29.png)

#### Sample ACF for data with trend and seasonal component

```text
a <- seq(1,10,length=200)
X <- 22-15*a+a^2+5*sin(20*a)+rnorm(200,20,2)
par(mfrow=c(2,1)) #dividing the page into 2 rows and one column
ts.plot(X, main = "Time Series With Significant Trend and Seasonality")
acf(X, main = "ACF Exhibits Seasonality + Slow Decay", lag.max = 60)
```

![](/Users/crystal/temp/.gitbook/assets/image%20%2839%29.png)

