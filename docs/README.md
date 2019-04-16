# Time Series Analysis on Sales Data

### Motivation
---

<p align="justify"> Time series prediction problems pose an important role in many domains and multi-series (More than one time series), multivariate (multiple predictors) and multi-step forecasting like stock price prediction of different symbols could help people make better decisions. However, these problems are quite hard to solve. </p>

<p align="justify"> Retail is an important business domain for data science and data mining applications. Sales forecasting is an essential task in retail stores. Being able to estimate the number of products that a store going to sell in future will allow store managers to prepare the inventory, the number of employees needed minimizes over and under stocking thereby minimizing losses and most importantly maximizes sales and customer satisfaction. Therefore forecasting sales taking into account all of the factors becomes essential. </p>

<p align="justify"> Given the background, we would like to analyze and identify the factors that affect the sales and predict patterns in the same for different stores over time. We make use of the sales data of 10 stores over the time period of 2 years and work towards forecasting future sales. </p>

We aim to approach this problem from two different perspectives:

- Treating the prediction of sales purely as a time series analysis and forecast sales using Autoregression Integrated Moving Average (ARIMA), LSTM and see how these two models could increase the forecasting accuracy.

- Viewing the problem as a Supervised Machine Learning problem by taking lags and calculating moving averages both on target and features. we would like to compare the relative performance of XGBoost to above time series models.


<p align="justify"> we would like to design a web application that provides an interface by which data scientists or store managers can use past sales data to forecast it from a selected date. In addition to allowing the user to retrain and tune three different time series models, the application also displays the model performance, past information and forecasted predictions visually. </p>


### Dataset
---
The dataset is sample sales information of 10 different stores over the time of 2 years from DataRobot Inc.

Features Available:

Store_Location 		- Different locations of the store [Categorical]
Date 				- Year, month and day of the sales of the stores [Quantitative]
Sales 				- Sales of different stores over time [Quantitative]
Store_Size 			- size of the store [Quantitative]
Num_Employees 		- Number of employees on that particular date and store [Quantitative]
Returns_Pct			- Return percentage [Quantitative]
Num_Customer		- Number of Customers in a store and on a particular Date [Quantitative]
Pct_On_Sale 		- Percentage on Sale [Quantitative]
Marketing			- Discount Information of the store on a date [Text]
Near_Xmas			- If a particular day is near to Christmas [Categorical]
Near_BlackFriday	- If a particular day is near to Black Friday [Categorical]
Holiday				- If a particular is a Holiday or not [Categorical]
Destination_Event	- If there is a destination event on that particular day or not [Categorical]
Econ_ChangeGDP		- Change in economy GDP [Quantitative]
Econ_JobsChange		- Change in jobs [Quantitative]
Annualized_CPI 		- Annual Consumer Price Index (CPI) [Quantitative]


### Getting Started
---
Install the dependencies for the web application using the python [requirements file](https://github.com/srjit/sales-time-series-analysis/blob/master/src/app/requirements.txt) by the command

```
pip install -r requirements.txt
```

### Retraining Models
---

Following are the descriptions of the hyperparameters for each model integrated into the application

- ARIMA

	* p - the number of autoregressive terms
	* q - the number of lagged forecast errors in the prediction equation.
	* d - the number of nonseasonal differences needed for stationarity
	
- XGBoost

	* learning_rate - Boosting Learning Rate. 
	* max_depth - Maximum tree depth for base learners.
    * n_estimators - Number of trees to fit.
  
- LSTM

	* learning_rate - learning rate of the optimizer. The default value is 0.01
	* optimizer - Optimizer used for the lstm model. This could be either sgd, rmsprop, adam. Adam seems to be the optimizer that provides best values for the metrics used.

### Visual Outputs
---

#### Model Performance

<p align="justify"> Doughnut chart describes the historical average sales at different stores. As the Store is an categorical variable, each value is encoded using a different color attribute. The arc length of each slice is proportional to the average sales of a particular location. The location lebel on each arc provide initial overview to the user on what each arc represents. On hovering over each location, we get the average sales of that store displayed in the area of inner circle with the location which provides on demand details. </p>

<p align="justify"> Onclick on the hovered store, links to the model performance evalution (Time Series Cross Validation) plot using line charts for that particular store using user selected model. </p>

<p align="justify"> Multiple line charts describe the model performance using forward validation of a particular store. This approach uses the input from user on the initial train end date, until which, data is considered to be as part of training data and next two months as the validation data (validation window period = 2 months). In the next step, we consider data until validation end date in first step to be part of trainig data (training data increased by 2 months) and next two months as validation data. This will be repeated for one more step. This is considered to be a practical approach as we validate and retrain model using the future data in real world. </p>

<p align="justify"> As the Sales and Time are quantitative variables, we have used position as channel which is ranked first in effective channel ranking by datatype for quantitative variables. As we have two attributes Actual and Predicted sales over the Y-axis, we used two different colors to encode the attributes where 'steelblue' represents the actual sales and 'tomato' represents the predicted sales value. This plot uses simple and effective ways to visualize the model performace as it makes use effecitve channels, marks, avoids the extra unnecessary dimension and minimizes the occlusion by using only to attributes at a given time. </p>

 
#### Area Plot for Visualizing Historic Data

The stacked area chart describes about the historical sales data for all the stores. Each store is encoded using a color attribute and it is aggregated month-wise. On Hovering over the Area plot on a particular store, we can get the details of the sales in a store for a particular day.
	
An Onclick on the selected store links to the sales forecast for the next 7 days after the forecast start date for a particular selected store.
	
#### Forecasting Predicitons

The waterfall plot provides a visualization of the predictions from the models integrated to the applications. The forecast date can be provided as one of the user inputs while the model is being trained/re-trained. 

The plot shows the variation of prices (up/down) and the percentage change in the prices from the prices from the previous day. An increase in sales is represented by a gray bar whereas a decrease is represented by an yellow bar.
 
### Running the app locally
---

Once the dependencies are installed, the app can be run locally with the command `flask run`. 

### Deployment
---

The app has been deployed on a heroku server at: [Sales Analyzer](https://sales-ts-forecast.herokuapp.com/)
