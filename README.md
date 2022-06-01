# project3

# Introduction
#This project generates trading signals using moving average crossover and an SVM model on a group of six stocks. 

# Technology
This project uses sklearn, numpy, pandas, yfinance, hvplot and matplotlib and is written in python.

# Description
Historical OHLCV data is pulled using the yfinance API for a list of six stocks. The code loops through the list, drops unnecessary data, and adds to a dataframe. The next section calculates 50 and 100 day moving avergaes and generates signals, which are added to the same data frame. AAPL price and signals are plotted in hvplot along with returns. Cumulative trading returns are plotted for all six stocks, with and without TSLA.

The next section applies an SVM model on the same six stocks to generate a daily signal. yfinance data is instead pulled into separate dataframes using a custom fuction and added to a dictionary with each ticker as a key. 50 and 100 SMAs are added as features for each ticker in the dictionary as well as a binary 1,0 for positive or negative daily return. A loop interates through the dictionary and scales, trains and tests an SVM model for each ticker with a 70/30 train/test data split. A separate loop calcuates cumulative return for model and actual returns during the testing window. Graphs are plotted for each stock along with summary statistics. 

### Random Forest Model
The random forest model was designed to produce trade signals that determine if a stock will go up or down tomorrow. Random forest classifiers train individual decision trees with randomized parameters and average the decision trees, making them resistant to overfitting. Random forests also pick up non-linear relationships well, which is useful when trying to predict stocks. 

An initial model was created to make the prediction and estimate the accuracy. Then two functions were created to attempt to more accurately predict the status of each stock tomorrow and backtest the results of the predictions to see how well the predictors performed.

The predict function required that the model have 60% certainty before classifying the stock to go up tomorrow. This was done in an attempt to make the model more accurate than the baseline model. The resulting model also included more predictors than the baseline model. These predictors included the addition of the mean closing price for the previous 2 days, week, 3 months, one year, and 4 years. Overall, the additional predictors did help increase the precision score of the model. 5 out of the 6 stocks ended up with precision scores above 50%, with two of the stock precision scores maxing out at ~55%. 

Next steps for this model would focus on the parameters of the random forest classifier. Adjusting the n_estimators and min_samples_split would be good starting places to attempt to build upon the model and make it more accurate. 
