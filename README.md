Final-Project-CS506

CS506 Final Project Report – [https://youtu.be/N8hSBmJJcU4?si=I6YtV1qTs7o9jRWm](https://youtu.be/N8hSBmJJcU4?si=fefODd4Jcil2HOkf)
Introduction

The objective of this project was to develop a predictive machine learning model capable of estimating retail product ratings using structured product and merchant attributes. The dataset included both numerical and categorical features such as price, number of reviews, shipping information, and merchant reputation metrics. There was also information on the details of the items and when they were released, what season, etc. Multiple modeling approaches were explored to evaluate the data and see if there could be any insights to report on.
2. Methodology

2.1 Random Forest Regression

A Random Forest Regressor was tested to determine whether a non-linear model could better capture hidden patterns in the data. This model was able to handle complex interactions between variables, but the improvement was still limited.

Feature importance analysis revealed that only a few variables — primarily price and review count — had measurable influence on the predicted rating. Even these variables showed weak predictive strength.

This indicated that the model limitation was rooted in the data itself rather than the algorithm.
Results:

Validation R²: 0.3246548656351851
Test R²: 0.48800541666666863
Validation MSE: 0.2119383108333315
Validation MAE: 0.3220333333333325

These results indicate that the model essentially learned to predict the average rating for most observations, providing little predictive value.

2.2 Testing the Model

Model didn't really work as well as it probably could. I think that this could be something that could be fixed with more time spent on it or more look into different models that could've possibly been used.

Results:

Predicted rating: [3.9]
Predicted rating: [3.9]
MSE: 0.16000000000000242
MAE: 0.400000000000003

The result shows that the prediction is about 0.4 points off from the true rating. That isn't terrible on a 5 point scale but it isn't good either. I think this model has the potential to be improved upon however it is hard to make a popularity prediction with the vast amount of attributes and trying to figure out which one is the best. I think proving popularity is a bit harder than proving the rating score which is why it was the first thing I did.

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
