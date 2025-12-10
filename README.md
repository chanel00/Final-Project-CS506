Final-Project-CS506

CS506 Final Project Report – [https://youtu.be/N8hSBmJJcU4?si=I6YtV1qTs7o9jRWm](https://youtu.be/N8hSBmJJcU4?si=fefODd4Jcil2HOkf)

1. Introduction

The objective of this project was to develop a predictive machine learning model capable of estimating retail product ratings using structured product and merchant attributes. The dataset included both numerical and categorical features such as price, number of reviews, shipping information, and merchant reputation metrics. Multiple modeling approaches were explored to evaluate which techniques could best capture the patterns influencing product ratings.

2. Methodology
2.1 Logistic Regression

Logistic regression was initially tested to explore whether ratings could be predicted using a classification-based approach. However, this model performed extremely poorly. One of the main challenges was the presence of categorical string variables, which logistic regression cannot process without feature encoding.

After applying one-hot encoding to categorical variables, the model still failed to produce meaningful predictions.

Results:

Validation R²: -5.1216 × 10⁻⁵

Test R²: -0.0003

Predicted Rating: [3.0052]

Mean Squared Error (Validation): 1.3327

Mean Absolute Error (Validation): 0.9995

These results indicate that the model essentially learned to predict the average rating for most observations, providing little predictive value.

2.2 Linear Regression

A linear regression model was then implemented to allow for continuous rating prediction. To handle categorical features, one-hot encoding was applied using:

X_encoded = pd.get_dummies(X, drop_first=True)


This preprocessing allowed the model to accept non-numeric data.

Results:

Validation R²: -2.1556 × 10⁻⁵

Test R²: -0.0003

Predicted Rating: [3.0107]

Mean Squared Error (Validation): 1.3327

Mean Absolute Error (Validation): 0.9995

Despite preprocessing improvements, the linear regression model also lacked predictive power and behaved similarly to logistic regression.

2.3 Random Forest Regression

A Random Forest Regressor was tested to determine whether a non-linear model could better capture hidden patterns in the data. This model was able to handle complex interactions between variables, but the improvement was still limited.

Feature importance analysis revealed that only a few variables — primarily price and review count — had measurable influence on the predicted rating. Even these variables showed weak predictive strength.

This indicated that the model limitation was rooted in the data itself rather than the algorithm.

2.4 Random Forest Classifier

To simplify the prediction task, ratings were converted into binary labels (high vs. low ratings). A Random Forest Classifier was then trained on this transformed target.

Results Summary:

The model began making distinct class predictions rather than predicting a single dominant class.

Overall accuracy: ~0.51

Performance was only slightly better than random guessing.

Confusion Matrix:

Predicted Low	Predicted High
Actual Low	32,604 (TN)	29,666 (FP)
Actual High	19,803 (FN)	17,927 (TP)

Interpretation:

Correctly predicted ~52% of low ratings.

Correctly predicted ~48% of high ratings.

False positives were frequent, meaning low-rated items were often predicted as high.

These results confirm that separating rating classes based on the available features is very difficult.

3. Visualization and Exploratory Analysis

To explore the structure of the ratings, visual and statistical analysis was performed using:

df['Rating'].hist(bins=10)
df['Rating'].describe()


The histogram revealed that ratings were tightly clustered around the mean, with very little variance. This explains why many models defaulted to predicting values near the average rating (~3.0).

Probability plots showed a regression trend hovering around 0.4, indicating model underconfidence — predicted probabilities rarely moved far from the midpoint, suggesting weak class separation capability.

4. Discussion

Across all modeling approaches, predictive performance was consistently weak. The limitations were not due to algorithm choice, but rather to feature limitations. The available variables (primarily price, review counts, and basic product attributes) failed to capture the complex human and qualitative factors that influence reviews.

Future improvements could include:

Sentiment analysis on written reviews

Product category or brand-level reputation features

Temporal trends such as seasonality

Customer-level behavioral or demographic data

With richer features, significantly stronger predictive performance would be expected.

5. Conclusion

This project demonstrated that traditional machine learning models — including logistic regression, linear regression, and random forest — struggle when the feature set does not strongly relate to the target variable.

While the Random Forest Classifier showed slight improvement, overall prediction strength remained low. The results highlight that product rating prediction is inherently complex and requires more expressive and detailed data sources.
