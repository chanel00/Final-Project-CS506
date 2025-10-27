# Final-Project-CS506
CS506 Final Project Report - [https://youtu.be/2uMxnRy20Mo](url)
1. Introduction
The objective of this project was to develop a predictive model to estimate product ratings using various features such as price, review count, and other categorical variables. Multiple regression and classification techniques were explored to determine which approach could most accurately predict ratings.

2. Methodology
2.1 Logistic Regression
Initially, a logistic regression model was applied to the dataset. However, the model performed poorly because it included string (categorical) variables that logistic regression cannot directly handle.
To address this, feature encoding was later implemented, but the logistic regression still failed to provide meaningful predictive power.
Results:
Validation R²: -5.1216 × 10⁻⁵


Test R²: -0.0003


Predicted Rating: [3.0052]


Mean Squared Error (Validation): 1.3327


Mean Absolute Error (Validation): 0.9995


These results indicate that the model essentially predicted the average rating for all entries, suggesting little to no correlation between the input features and the target variable.

2.2 Linear Regression
Next, a linear regression model was implemented. To handle categorical data, one-hot encoding was used:
X_encoded = pd.get_dummies(X, drop_first=True)

This conversion allowed the model to process text data numerically.
Results:
Validation R²: -2.1556 × 10⁻⁵


Test R²: -0.0003


Predicted Rating: [3.0107]


Mean Squared Error (Validation): 1.3327


Mean Absolute Error (Validation): 0.9995


The results were very similar to those of logistic regression, again showing almost no predictive power.

2.3 Random Forest Regression
A Random Forest Regressor was then tested to determine whether a non-linear approach could improve results. Unfortunately, this model also produced similar outcomes, confirming that the available features lacked the necessary predictive strength.
Feature importance analysis revealed that price and review count were the only attributes with any measurable influence on rating—but even these effects were minimal.

2.4 Random Forest Classifier
To simplify the task, the rating variable was converted into binary categories (high vs. low ratings), and a Random Forest Classifier was applied.
Results Summary:
The model was no longer predicting “all 0s”; it now made distinct predictions for high and low ratings.


Despite this improvement, overall accuracy remained low (~0.51), indicating weak separation between classes.


Confusion Matrix Analysis:


Predicted Low
Predicted High
Actual Low
32,604 (TN)
29,666 (FP)
Actual High
19,803 (FN)
17,927 (TP)

Interpretation:
The model correctly predicted ~52% of low ratings and ~48% of high ratings.


False positives (predicting high rating when it was actually low) were frequent.


The model demonstrates that product rating prediction is inherently noisy and that the selected features do not fully explain the outcome.



3. Visualization and Exploratory Analysis
To better understand the distribution of ratings, the following were used:
df['Rating'].hist(bins=10)
df['Rating'].describe()

The histogram and descriptive statistics revealed that ratings were tightly clustered, with minimal variance. This explains why models tended to predict values close to the average rating (~3.0).
A regression line around 0.4 in probability plots indicated underconfidence — the model’s predicted probabilities hovered around 40% for class 1, showing that it struggled to distinguish between high and low ratings.

4. Discussion
Across all modeling approaches, predictive performance was weak. The primary cause was not model choice but feature limitation. The available variables—mainly price, review count, and categorical text fields—did not capture the complexity influencing product ratings.
Future work could focus on incorporating more descriptive and behavioral features such as:
Sentiment analysis of review text


Product category or brand reputation metrics


Temporal trends in ratings (e.g., seasonality)


Customer demographic information


These additions would likely provide more predictive power and allow for more meaningful model development.

5. Conclusion
This project demonstrated that traditional regression and classification models (logistic regression, linear regression, and random forest) perform poorly when the predictor variables lack strong relationships to the target outcome.
While the random forest classifier showed marginal improvement, the models overall confirmed that rating prediction is complex and requires richer, more informative data.

