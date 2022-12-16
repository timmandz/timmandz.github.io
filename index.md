## Abstract

The stock market has huge potential for experimenting with deep learning. If one is able to accurately predict future stock prices, money would no longer be an issue. In this project we use compare different model architectures ability to forecast the stock market in the hopes of finding out which model architectures have potential, and which model architecture should best be avoided. 

## Problem Statement

For our final project, we analyze 2 single-shot prediction models: an LSTM model, and a convolutional mode, as well as an autogregressive LSTM model, to see which model, given only historical data of a particular stock, performs the best in predicting future stock prices. We hypothesize that despite many claims against being able to make accurate stock price predictions, we will be able to come up with a (relatively) simple model that might give some direction into the trend of a stock price for the coming days. 

## Related Work

There's various research out there regarding stock price prediction. One paper that uses very similar methods to what we do and acts as our inspiration for this project can be found [here](https://arxiv.org/ftp/arxiv/papers/2009/2009.10819.pdf). It analyzes the same issues

## Methodology

We get all of our stock price data using yFinance, which is an open-source Python library that allows easy and free access to stock data from Yahoo Finance. We can request data for any company and any time period. The data includes features such as open price, closing price, the day's high, the day's low, the adjusted close, and volume, at any given date. To simplify, we only keep the "Closing price" (and date). Thus, we want our models to predict the future closing price of a given stock, using only historical closing price as input. In future work, it may be worthwhile to consider other features and their affects on the model's accuracy, although we suspect that they are all highly correlated and that including all features are probably redundant.

First, will pull all closing prices for AAPL (Apple Inc) between X and Y. We split the data into training, validation, and test sets using the ratios (70%, 20%, 10%). (include image here). We do not shuffle the data before splitting to maintain it's orginal order, and to ensure that the validation and testing sets are collected after the training set, which mimics how one would use the model in the real world. 

We then normalize all data using the mean and standard deviation of the training set. In the future, it might be worthwhile to use rolling averages for this normalization process; however, in the interest of simplicity we use a simple average.

We then preprocess our training set into a format suitable for training. Since we want our models to take historical stock prices as input, and predict future stock prices as output, we have to use the same format during training: From our training set we create two sets, inputs (x) and labels (y). Each sample in our inputs consists of a window of consecutive samples from the data. The size of the window is a tunable parameter (INPUT_WIDTH), and defines how many consecutive days our models will use to make each prediction. Each sample in our labels set is also a window of consecutive sample from the data, where the window is of size LABEL_WIDTH, which defines how many days the model will predict for each prediction. Finally we also have parameter OFFSET which defines how many days into the future the predictions should be from the input. For simplicity we always used OFFSET=1.

For example, to make a single predicition (LABEL_WIDTH=1) one day (OFFSET=1) into the future, given six days of history (INPUT_WIDTH=6), we would need a window like this:

![window example explanation](raw_window_1d.png)

Note also that a single pair (input_0, labels_0) overlaps

## Experiments/evaluation

The simplest model you can build on this data is one that predicts a single feature's value one time step into the the future based on current conditions. So we start with building a model to predict the stock price just one day in advance.

## Results

## Examples

## Problems and Future Work

## Video

## Team Members

Tim Mandzyuk, Ludvig Liljenberg
