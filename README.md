# Deposit-opening-classification-problem

## Data Retrieval and Cleaning

We have data for 41,188 participants in the marketing campaign, with 20 columns of data.
We clean the column headers by replacing the periods in the headers with underscores and To maintain data quality, we filtered out rows with missing or NULL values in specific columns. This step ensured the reliability of our analysis.
Ran Univariate and Bivariate Distributions of the data, we notice class imbalance and multicollinearity in the data, which were dealt with grouping, transformation and feature selection.

### Univariate Distributions

For numerical variables: Except 'AGE’ (which his near normally distributed) all other variables are not normally distributed.
These variables will be grouped into two categories according to their distribution: PDAYS and EURIBOR3M
Others were normalized using 'StandardScaler'.

For categorical variable: We can see there is high unbalance between categories in certain variables, they are grouped for example: 
Education: college VS. non-college
Month: special months (Mar. & Sep. & Otc. & Dec) VS. others

### Bivariate Distributions

![image](https://github.com/Vishweshpurohit/Deposit-opening-classification-problem/assets/111001693/196cd3bd-49ac-40d0-87eb-ad9db00e2bb0)

We check for the impact of different categories on the target variable “y”. From these we could see which categories impact users decision to subscribe, we are able to dwell deeper into building  profiles of our customers.
We see that education_udf , maritial status , month can be looked into to provide insights

We see that in each and every one of the features there is a class imbalance, we see that there is more data for y = no as compared to y = yes.
Because of this we will have to look for evaluation metrics and machine learning models which could take this into consideration

### Correlation - Collinearity Problem

![image](https://github.com/Vishweshpurohit/Deposit-opening-classification-problem/assets/111001693/7ff83a51-5d64-44e8-849b-4732fc6a3209)

We see high linear correlation exist in these  6 pairs:
Emp_var_rate VS. cons_price_idx
Emp_var_rate VS.euribor3m
Emp_var_rate VS. nr_employed
euribor3m VS. cons_price_idx
euribor3m VS. nr_employed
Pdays VS. previous

We deal with these 3 variables to eliminate the collinearity problem:
Emp_var_rate: We remove this variable
Euribor3m: Change to categorical
Pdays: Change to categorical

## Feature Engineering

### Data Transformation Process

| Transformation Task                                               | Implementation Details                                      |
|---------------------------------------------------------------------|-------------------------------------------------------------|
| Transforming categorical data into numerical format                | Utilized `StringIndexer`, `LabelIndexer`, and `OneHotEncoderEstimator` to convert 12 columns into vectors. |
| Standardizing the data                                             | Applied standard scalar to bring all predictor variables to the same scale, ensuring no single predictor has a weighted impact due to the scale of measurement. |


### K means clustering

Once we complete preparing the Data using one-hot encoding and vector assembler, we feed them to a k means clustering model, we assign them to 4 clusters, due to 4 groups we could identify during our bi variate analysis

## Models

Model 1: Logistic Regression :We select this model since it provides a clear probability estimation for customer subscription, aiding in precise resource allocation for marketing strategies. This model is also easier to explain than many others

Model 2: Decision Tree : We select this model since it offers interpretability by illustrating decision paths, facilitating actionable insights for marketing strategies.

Model 3: Random Forest : We try this model since it would help with reducing overfitting, with the issue of class imbalance, random forest can  leverage ensemble learning for more robust predictions

Model 4 Gradient Boosted Tree:  We use GBT since it builds sequential models to correct errors of preceding models, improving accuracy and capturing complex relationships we might have missed

Model 5: Factorization Machine Classifier: We use this since it handles sparse data efficiently, from our research we saw that many recommendation systems use this model due to its high accuracy in predicting complex purchasing behaviour.

## Model Comparision

![image](https://github.com/Vishweshpurohit/Deposit-opening-classification-problem/assets/111001693/7790e5ae-3895-4ac1-a36a-4fc84392a955)

We look at the TP values for the all the models, as it is the most important validation parameter for this study.

## Model Selection

![image](https://github.com/Vishweshpurohit/Deposit-opening-classification-problem/assets/111001693/8b8f7f66-3aa0-4fc9-af56-6732e38dd26d)

We look at the simplest model with the highest AUC values as our model, since logistic regression gives us 92% AUC which is not much lower than GBT at 93%  and is easier to explain to stakeholders we select the logistic regression as our final model

## Conclusion

Based on the EDA, we see a higher loan rate among
1. Highly educated: Users in with higher literacy have higher subscription rate among different categories
2. Single users: People have have not married even once s    score a higher yes rate.
3. Months: people tend to react better to marketing campaigns during the certain months

## Recommendations

For highly educated: Target marketing strategies that can help users gain discounts on their future investments, highly educated users also would be tech savy so partnering with tech firms to offer deals could be efficient 
For single users: Create campaigns that appeal to their lifestlye, this could include deals adding value to their individual portfolio
For certain months :Plan and time marketing campaigns to coincide with March , September , October and December, this could look like seasonal offers or promotions that align with festivals 








