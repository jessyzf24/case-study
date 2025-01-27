# Case Study

## Data Processing Overview:
The dataset includes 4 tables with information on 1,615 users. Every user has account details, most have inflow/outflow data, and 60% have sales and revenue information. For the remaining 40%, one assumption is to treat them as negative samples—i.e., users with no sales or revenue data. However, upon reviewing the sales data for the 60% with records, we found 400 users already showing no sales (negative samples). This leaves us with two main approaches. One is to use the 60% of users with data as the training set and the 40% as the test set. However, since the test set lacks labels, it would be impossible to evaluate test accuracy. Another option is to apply unsupervised learning, clustering users based on their attributes and estimating sales based on the closest centroids. The approach detailed below follows the first option.

## Building Propensity Models:
We are focusing on three offers: mutual funds, credit cards, and customer loans. Therefore, we developed three binary classification models to predict the likelihood of each customer accepting one of these offers. Given the small dataset, overfitting is a risk, so I applied cross-validation to mitigate this. Specifically, I used 5-fold cross-validation, where each fold serves as the test set once, and the remaining four are used for training. Additionally, we can create regression models to estimate the potential revenue each client might generate. However, due to time constraints, I used the average purchase amount for each product group instead of building detailed regression models.

## Handling Constraints:
A key constraint is that each client can only receive one marketing offer. Therefore, when a client is predicted to be eligible for multiple offers, we must select the one with the highest predicted probability. By comparing the scores from the three classification models, we assign the offer with the highest score to the client. Another limitation is the contact quota, which requires ranking clients based on the highest probability across the three models and selecting the top 15%. Using a default threshold of 0.5, I identified 92 clients who qualify for at least one offer, which is close to the target limit.

## Optimizing Total Revenue:
Theoretically, we can create a revenue function that aggregates the potential revenue from all clients. By adding a negative sign, we can transform the problem of maximizing revenue into a minimization problem.
