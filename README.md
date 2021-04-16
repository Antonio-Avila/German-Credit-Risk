# German Credit Risk

### _Disclaimer:_
The dataset used for this project is outdated and cannot be used for use today. It was originally collected during the mid 1990s, shortly after the reunification of Germany. Thus, it is likely to give us a skewed look of the typical customer base at the time, given the likely influx of new customers coming from newly unified side. For example, a bank located in Western Germany may see a influx of Eastern Germans applying for credit lines now that they are able to freely travel across what used to be the Eastern/Western Germany border. Moreover, the currency used at the time was the Deutsche Mark, predating their adoption of the Euro.

### _Goal:_
The goal of this project was to analyze a dataset containing the financial records of the bank's customers in order to predict whether a new customer would be considered "good" or "bad". This consideration is important since it gives us an insight into whether the potential customer is likely to repay their loan or default. To achieve this, we want to create a model to predict the probability a customer is likely to default on a loan instead of only predicting whether the customer will be a "good" or "bad" one. Assuming the model is adequate, this allows the lenders to spend less resources on the "good" customers who are likely to repay their loan and focus on the ones likely to default according to the model.


The dataset can be found at: https://archive.ics.uci.edu/ml/datasets/Statlog+%28German+Credit+Data%29


### _Approach:_
The approach was simple.
- Began by cleaning the original dataset and giving the categorical variables meaningful names and state levels.
  - some information was lost due to discretization, for example, binning of numerical variables such as the amount of money in one's savings/checking account
- EDA revealed a few trends and variables that might be helpful in predicting the probability a customer will default on a loan as well as some potential multicollinearity.
- fitted a few simple models on the raw data to get a baseline
  - led to poor performance
- After some light feature engineering, it was time to address the most pressing issue

#### The Problem
Ideally, a bank wants to maximize its number of good customers while minimizing the number of bad customers. Due to the nature of the problem, this causes datasets like these to have highly imbalanced classes, e.g., there are over 2 times as many good than bad customers in the dataset. This is bad for training models since it encourages them to learn as much as possible from the larger class while learning next to nothing from the smaller class. There is not enough information on the lower class for the model to be able to accurately distinguish patterns between the 2 classes and be of actual use. Without


# Hello
