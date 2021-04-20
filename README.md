# German Credit Risk

### _Disclaimer_
The dataset used for this project is outdated and cannot be used for use today. It was originally collected during the mid 1990s, shortly after the reunification of Germany. Thus, it is likely to give us a skewed look of the typical customer base at the time, given the likely influx of new customers coming from newly unified side. For example, a bank located in Western Germany may see a influx of Eastern Germans applying for credit lines now that they are able to freely travel across what used to be the Eastern/Western Germany border. Moreover, the currency used at the time was the Deutsche Mark, predating their adoption of the Euro.

### _Goal_
The goal of this project was to analyze a dataset containing the financial records of the bank's customers in order to predict whether a new customer would be considered "good" or "bad". This consideration is important since it gives us an insight into whether the potential customer is likely to repay their loan or default. To achieve this, we want to create a model to predict the probability a customer is likely to default on a loan instead of only predicting whether the customer will be a "good" or "bad" one. Assuming the model is adequate, this allows the lenders to spend less resources on the "good" customers who are likely to repay their loan and focus on the ones likely to default according to the model.


The dataset can be found at: https://archive.ics.uci.edu/ml/datasets/Statlog+%28German+Credit+Data%29


### _Approach_
The approach was simple.
- Began by cleaning the original dataset and giving the categorical variables meaningful names and state levels.
  - some information was lost due to discretization, for example, binning of numerical variables such as the amount of money in one's savings/checking account
- EDA revealed a few trends and variables that might be helpful in predicting the probability a customer will default on a loan as well as some potential multicollinearity.
- fitted a few simple models on the raw data to get a baseline
  - led to poor performance
- After some light feature engineering, it was time to address the most pressing issue

#### The Problem
Ideally, a bank wants to maximize its number of good customers while minimizing the number of bad customers. Due to the nature of the problem, this causes datasets like these to have highly imbalanced classes, e.g., there are over 2 times as many good than bad customers in the dataset. This is bad for training models since it encourages them to learn as much as possible from the larger class while learning next to nothing from the smaller class. There is not enough information on the lower class for the model to be able to accurately distinguish patterns between the 2 classes and be of actual use. Without some way to balance the two classes, the model may appear to be performing well but in actuality it may be because of the imbalance classes. In the most extreme case, it may be predicting everything to be the in the larger class, and due to the higher number of cases, it may yield a decent accuracy score.

It is incredibly important to solve this problem since it could be difference between a model taking on too many and approving an acceptable amount of those "bad" credit that will default on a loan. Taking on too many bad borrowers could lead to losses ballooning, putting the company in a very precarious situation.

There are a few different approaches to counteract this problem.
- **Under-Sampling:** balances the classes by sampling from the larger class until we have an equal amount of cases in each class.
  - it has the disadvantage of loosing information due to "discarding" of samples
  - it may not be a suitable choice if the number of observations in the smaller class is too small, not leaving enough data to train the model on
- **Over-Sampling:** Scales "up" the smaller class by randomly sampling from them until there is an equal amount in each classes
  - the disadvantage of this method is that because we have to sample from the smaller class to scale it up, there will very likely be multiple occurrences of the original observations, adding more weight to those observations
- **Other Techniques:** There are other approaches to tackle the imbalanced classes problem
utilizing a hybrid approach of combining under-sampling with the simulation of new data. Such methods include the *ROSE* and *SMOTE* algorithms.


Although a logistic regression model with over-sampling performed well in the training set, the maximum accuracy score I could receive on a "new" dataset, the testing set, was about 73%. The good news is that the drop in performance between the training and testing sets was negligible. The model performed almost just as well in both datasets, and more importantly, it was able to distinguish ~69% of new "bad" borrowers.

This could be further improved by training more complex models such as a neural network. The downside in a neural network is the loss of interpretability. Interpretability is the sole reason I focused on the logistic regression model and attempted to maximize its performance. It plays a very important role, especially in a sector such as the financial sector that is regulated. The need to explain what is affecting decisions and how much of an effect a factor has on the outcome is invaluable. Though, there should be an asterisk on such explanations when using regulated models as I did in this case. The bias introduced to the model using an elastic net and lasso regularization to help improve performance distorts the results. In normal GLM models, the intercepts explain how much a factor affects the response variable. To improve performance, regularization can be introduced to the loss function to help find coefficients that create a more accurate model and/or to help with feature selection. The downside, as mentioned above, by introducing bias into the model, the interpretability normally applied to non-regularized GLM models should be taken with a grain of salt.


## What now?
Coming into this project, I had hoped to apply techniques used in finance such as Extreme Value Theory and Value at Risk to get an idea of how to apply such concepts and to further explore what a potential loss could be. Unfortunately, I do not think I have enough data to achieve this.
