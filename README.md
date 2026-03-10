## Repository: UCB\_Required\_Assignment20\_1

### Assignment: Required Capstone Assignment 20.1

### Title: Predicting Stock Market Betas for Equity Pairs

### Author: Bart Rothwell

### Date: 3/10/2026

#### Link to Jupyter Notebook with Exploratory Data Analysis

https://github.com/bartrothwell/UCB\_Required\_Assignment20\_1/blob/main/RequiredAssignment20\_1\_Rothwell.ipynb

#### Introduction and Research Question

This README file summarizes the exploratory data analysis performed for my Capstone Project, in which I investigate the relative price movements of pairs of equities traded on the US stock market, and attempt to predict the future relationship between them as expressed by their “Beta”, defined as the ratio of the price change of one equity to the price change of the other.

#### Motivation

Knowing the Beta of one stock to another is important to stock market traders so that they can calculate a “hedge ratio” for the two stocks – the number of shares of one stock they want to be short in order to offset a long position in the other stock, to minimize their risk when doing a pair trade in which they expect one stock to outperform the other.

#### Data Source

In order to calculate historical Betas for each trading day, I need to use data sampled intraday at regular intervals (for example, every one minute) during regular trading hours. I have selected Databento (https://databento.com/) as the data vendor for this project. This vendor provides clean, easily downloadable datasets of one-minute intraday Best Bid \& Offer (BBO) data at one-minute intervals for all the major equities traded on US stock market exchanges.

#### Method

* First, I will calculate the historical Betas from the intraday price data for each trading day for each pair of equities to be investigated, as the target for prediction.
* These Betas will form a time series for each equity pair, so my next step will be to do a time series analysis of the Betas (and the differences between successive Betas) to look at their autocorrelations (with ACF plots) and determine the nature of the time series.
* Then I will use a linear regression model to predict the Beta for each trading day from the Betas on previous trading days for each equity pair, and attempt to beat a baseline model that just predicts that each day's Beta will be the same as the last day's Beta for that equity pair. Note that due to time limitations, I will not be incorporating additional data as input features as I had originally proposed, or investigating more advanced modelling techniques. Instead, I will focus on determining the optimal number of lagged Betas to use for the prediction problem, for each pair of equities investigated.

#### Initial Results

* Plot of Initial Results

!\[](images/ModelPerformance.png)

* For my exploratory data analysis, I looked only at the XLK/SPY equity pair. My primary finding from this initial analysis is summarized in the plot above, which shows that by using the Betas for the previous 20, 10, or 5 trading days as inputs to a linear regression model, I was able to predict the next day's Beta more accurately than if I just predicted that each day's Beta would be the same as the last day's Beta. The MSE scores for the baseline model and the three regression models were as follows:

  * MSE for baseline model (predict last): 0.0197077
  * MSE for model using 20 lagged betas:   0.0159429
  * MSE for model using 10 lagged betas:   0.0158583
  * MSE for model using  5 lagged betas:   0.0162413

* A closer look at the linear regression coefficients for the trained models shows that the ideal number of lagged Betas is probably between 5 and 10.

#### Next Steps

* Based on this analysis, I will take a closer look at how performance changes as we look at different numbers of lagged Betas. I will also incorporate data from additional equity pairs, to see if I can pinpoint a model that performs best across all the equity pairs investigated.
