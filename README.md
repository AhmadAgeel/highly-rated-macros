# Highly Rated Macros: What do macros tell us about a recipe's average rating?

## Introduction
This project helps contributors to food.com know what types of recipes are expected to get rated higher.
## Data Cleaning and Exploratory Analysis
I left-merged the recipes dataset with the interactions dataset which contains reviews and ratings on recipes

I replaced ratings of 0 with null values because the ratings can only be integers 1-5 and because having these missing values as zeros--and not null--will falsely bring the average down.

using the merged dataset with null missing ratings I was able to find the average rating for each recipe--some of which have null values.

I added average recipes to the merged dataset

[cleaned.head()]


[singe dist and explaination]

[2col dist and explanation]
## Assessment of Missingness
I believe the rating column is NMAR because some people only rate when they're not satisfied
## Hypothesis Testing
Null Hypothesis: High and low-carb recipes take similar time to prepare on average (any recipe with <30% PDV is low)
Alternative Hypothesis: Low-carb recipes are faster to prepare on average

Test Statistic: Difference in means

My significance level was 0.05=5% and the p-value was 0.1184=11.84% >= 5% so I failed to reject the null.
## Framing a Prediction
I will try to predict the average rating for recipes. This is a regression problem. I will be using the default scoring metric R^2.

I want contributors to use this before posting a recipe so we will only have access to information in the recipes dataframe at the time of the prediction
## Baseline Model
Model: Decision Tree Regressor

quantitative: it will use all the nutrient columns as-is

This model has a test root mean squared error of about 0.69 which is a good first start

## Final Model
nominal: It will use `CountVectorizer` (with `binary=True` and `stop_words='english'` to disregard common English words) on the name column to see which words correspond to different average ratings.

This improves prediction because now the type of recipe is taken into account.

I did a grid search with `cv=5` to find the best `max_depth` and it turned out to be `max_depth=5`.

## Fairness Analysis
I want to know if my model is fair and predicts as good for both long and short cooking times.

Null Hypothesis: Our model is fair. Its R^2 is the roughly the same for long and short recipes, and any differences are due to random chance.

Alternative Hypothesis: Our model is unfair. it performs better for ... recipes
