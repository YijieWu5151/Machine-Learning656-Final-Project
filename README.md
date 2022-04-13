# Machine-Learning656-Final-Project

IEEE-CIS Fraud Detection
(https://www.kaggle.com/c/ieee-fraud-detection) 
1.	Problem Statement
1.1Business Framing
①Current Situation: 
Fraud transaction happens every minute around the world. Although the fraud prevention system is actually saving consumers millions of dollars per year, it can be improved with more accuracy.
②Purpose of building the model: 
This machine learning model can provide higher accuracy fraud detection for online transaction.
If successful, it can improve the efficacy of fraudulent transaction alerts for millions of people around the world, helping hundreds of thousands of businesses reduce their fraud loss and increase their revenue. 

1.2Data Description
The data comes from a real-world e-commerce transactions company and contains a wide range of features from device type to product features. 
We are predicting the probability that an online transaction is fraudulent, as denoted by the binary target isFraud.
 


2.	Technical Approach
There are two steps to build the model. First, I preprocess data, including handling missing data, encode categorical variables, PCA to reduce dimension. Then, I use five different approaches to predict fraud, including logistic regression, bagging trees, random forests, gradient boosting, XGBoost.
2.1	Data preprocessing
①	Import and merge the data: 
After I import the appropriate libraries and data, I merge identity and transaction to one data frame left joined by TransactionID. The computation on the whole data set is too expensive, so I randomly select a subset of size 5000 for demo. 
 
Now, training dataset has 5000 observations and 434 features while test dataset has 506691 observations and 433 features.
②	Handle missing values: 
I drop features with high proportion (70%) of missing values. Then, I fill missing values in categorical variables with their mode and fill missing values in numerical variables with their mean.
 
After deleting features with high proportion of missing values, there are 223 features.
③	Encode categorical variables: 
I try two different ways: numeric encoding and binary encoding. Numeric encoding (label encoding) simply assigns a value to each category. Binary encoding hashes the cardinalities into binary values. (Here is the reason why I do that: https://medium.com/data-design/visiting-categorical-features-and-encoding-in-decision-trees-53400fa65931)
④	PCA to reduce dimension: 
Although PCA can reduce dimension and computation time, the result showed that the prediction performance with PCA is worse. So I will not use the data after PCA to fit the model and make predictions in the modeling part.
⑤	Save processed data
 
The data is clean now.

2.2	Modeling
①	Logistic regression: 
The prediction score is 0.713617.
 
②	Bagging trees: 
I use RandomForestClassifier and set max_features="auto", which means max_features = n_features, so it is bagging.
 
③	Random forests: 
Let's first do parameter tuning. Other than max_features (the number of variables considered at each split), the parameter n_estimators (the number of trees) is also important. However, the prediction performance will increase with the increase of n_estimators, so we should select the highest n_estimators as long as our machine can compute it. I try different parameters (max_features and n_estimators) and get the prediction scores (evaluated by AUC) as following.
 
④	Gradient boosting: 
At first, let's try gradient boosting with default parameters. The prediction score on test data set is 0.891210.
 
Now let's do parameter tuning. The parameters n_estimators and learning_rate are correlated, so we need to tune them together. Let's use grid search to find the best number of weak learners (n_estimators) and the best step size (learning_rate). After parameters tuning, the prediction score (by AUC) on test data set is 0.919523. It is better than that without parameters tuning.
⑤	XGBoost: 
The prediction score on test data set by XGBoost with default parameters is 0.900976, and 0.931355 with the parameters tuned by GBT.
 

3.	Results
From the results, we can see the prediction score (evaluated by AUC) of XGBoost is the highest and most accurate, around 0.93.

4.	Conclusion:
I think the model can be useful and help improving accuracy of fraud detection.
 
The superiority of my approach to relevant benchmark methods:
①	 I compare five different approaches and choose the most accurate one.
②	 I do parameter tuning before running the models.
③	 I try to use PCA to reduce dimension and computation time. But as the result shows that the prediction performance with PCA is worse. So I don’t use the data after PCA to fit the model and make predictions in the modeling part.
④	 In data processing, I drop features with high proportion (70%) of missing values and encode categorical variables.
