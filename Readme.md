# Non Retail Sector Sales Time Series Forecast

Can we predict the growth of Sales in the Non Retail Sector.

During the course of history man has always been able to go to a store and purchase items, however over time there has been a drastic need of comfort and security and there has been a rise in demand for non-store retail. Establishments in this sub sector include mail-order houses, vending machine operators, home delivery sales, door-to-door sales, party plan sales, electronic shopping, and sales through portable stalls. As the world around us evolves we have seen many different events cause major pitfalls in sales and decline in retail, many of the recent events have caused a polar opposite effect on such non retail sectors. There is a need to study the potential exponential growth of this sector and take a look at the seasonality between this. 

## Data
Federal Reserve Economic Data is a database maintained by the Research division of the Federal Reserve Bank of St. Louis that has more than 816,000 economic time series from various sources. The Federal Reserve is in charge of making economic decisions that have a large scale impact on the econommic infrastructure of the United States and contains many different APIs on the current state. We have pulled the time series data from FRED for the nonretail sector which is encoded as RSNSR. This data is refreshed daily on the FRED database. We have two columns which contain the dates and the value of the sales of the non retail sector. The data ranges from 1992 to 2019. 

![image](https://user-images.githubusercontent.com/69598569/162645716-ccf9097a-745b-4dc4-8a2d-d72e1a46048d.png)

## Method
We will be using ARIMA and ARIMAX Models in order to find out the order of the data and fit it to the training data and test it on a subset of the data. We will then use it to forecast on to future months. We will start but getting the data stationary using the Augmented Dicky Fuller test and then fitting to the correct model.

## Data Cleaning
We received the data in datetime and int format which allowed for easy cleaning. However the data was not stationary as can be told by the graph below

![image](https://user-images.githubusercontent.com/69598569/162645802-3d7fabfe-0541-4e9b-b3d1-2b318cec0748.png)

## EDA and Preprocessing
EDA showed us that the sale of nonretail goods was constantly growing. We looked at a subset of the data and we saw that there is not a lot of seasonality and the data is not stationary. This subset can be seen below.

![image](https://user-images.githubusercontent.com/69598569/162645899-09b0f30f-d7b7-4ce2-b456-d3cc23ddaf41.png)

Using the AD Fuller test we received a value of -3.45. We needed to get the data stationary.

We then performed a percent change to allow for room for stationary data. This worked well to create stationary values and the AD Fuller test was .007. However the data could be more stationary.

We calculated the difference of the values to create a more stationary and steady data. The AD Fuller Test p value was 6.1e-11 which was close to 0. Our data was ready to be modeled.

## ML and Algorithms
We worked with the SARIMAX model initially from the statsmodel library. We used an initial simple 1,0,0 model in order to test a simple model for this data. 

![image](https://user-images.githubusercontent.com/69598569/162646112-c10d62ea-bdd4-490e-ae33-73e83c109ce9.png)

The AR1, MA1 coefficient and the bias term or intercept were not at all significant.

Our Model did a decent job on the training set however did not make any good predictions. As portrayed below.

### Training
![image](https://user-images.githubusercontent.com/69598569/162646202-e56af68a-59dc-46f9-8e07-4f2d3d37570c.png)

### Forecasting
![image](https://user-images.githubusercontent.com/69598569/162646219-d37ccd14-b40a-41ea-9ec1-2973a0faab28.png)

The auto correlation functions showed no tailing off and therefore we could tell that this data required a model of a higher order.

![image](https://user-images.githubusercontent.com/69598569/162646333-ca7f68cc-43bb-4f7d-ba43-b9d837933644.png)

Using the AIC and BIC pipeline to check for optimal values we found that the optimal values were 2,0,2 ARMA model. This provided with better forecasting and good plot diagnostics.

![image](https://user-images.githubusercontent.com/69598569/162646427-5708e9df-0c71-4e65-ae5f-d07a3c691d05.png)

### Algorithm

There was some seasonality to this data but we could not pinpoint the exact amount however we imported a package pmdarima which allows the model to pick the best parameters for the seasonal ARMA model as well.
Running this model we received the following result based off the lowest AIC.

![image](https://user-images.githubusercontent.com/69598569/162646512-e5e833fe-5ed0-4716-a106-7099c8ad5f63.png)

This was different that the previous Model we ran and therefore leads us to believe there is some seasonality in the mix.

![image](https://user-images.githubusercontent.com/69598569/162646542-346dea8b-bfdd-4da9-a3f0-e43cd818a718.png)

Using the forecasting graph and getting the values we were able to forecast the following sales in December of 2021.
![image](https://user-images.githubusercontent.com/69598569/162646583-60ce6214-dfbb-48b4-a6be-04ff73da2177.png)

## Recommendations

The world of economics is very complicated and there are a lot of factors that go into forecasting different metrics. Using factors that affect sales such as COVID can give us a lot of insight and being able to add these metrics to the data will provide a lot of insight into this sector. We are able to achieve a lot more using the information that is available and build out more accurate real world models using different metrics such as these.


