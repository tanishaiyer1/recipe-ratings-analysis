# Analysis of Average Recipe Ratings
**By: Tanisha Iyer and Reva Agrawal**

## Introduction 

Whether we are cooking dinner at home or looking up recipes for special occasions, everyone has their go-to favorites and opinions about what makes a dish great. In today's health-conscious world, understanding the factors that influence our food choices is more important than ever. While taste and personal preference play significant roles, the nutritional content of a recipe can also impact its popularity. The central question of our project is: **"Do the nutritional factors of a recipe significantly influence its average rating?"** By investigating this question, we can gain valuable insights into the interplay between health and taste. Our findings could empower individuals to make informed dietary choices, inspire recipe developers to create healthier and more appealing dishes, and guide the food industry in developing innovative and nutritious products.

We are working with two datasets for this project. The first, 'Recipes', contains different recipies and information about them, and the second, 'Ratings', has the ratings and reviews of the recipies. Below are the columns of the two datasets:

### Recipes 

|Column				| Description	|
--------------------| ------------- |
| `name`			| Recipe name 	|
| `id`				| Recipe ID  	|
| `minutes`			| Minutes to prepare recipe |
| `contributor_id` 	| User ID who submitted this recipe |
| `submitted` 		| Date recipe was submitted |
| `tags` 			| Food.comtags for recipe |
| `nutrition` 		| Nutrition information (calories, total fat, sugar, sodium, protein, saturated fat, carbohydrates) |
| `n_steps`			| Number of steps in recipe |
| `steps` 			| Recipe steps, in order
| `description`		| User-provided description |

### Ratings

|Column				| Description	 |
--------------------| -------------  |
| `user_id`			| User Indicator |
| `recipe_id`		| Recipe ID  	|
| `date`			| Date of interaction |
| `rating` 			| Rating given |
| `review` 			| Review text |


## Data Cleaning and Exploratory Data Analysis

We first had to clean the raw data. We started by merging the two datasets on id and recipe_id. We then handled all missing rating by replacing all zero ratings with NaN values. Next we Converted the nutrition column from a string representation of a list to individual numerical columns for each nutrient and then removed the original nutrition column. We also calculated the average rating for each recipe and added it as a new column. Next we added binary indicators for the presence of vegetables (has_veggies) and whether the recipe is tagged as healthy (is_healthy). 

Here are the relevant columns of the processed dataframe:

| Column        | Description                                                |
| ------------- | ---------------------------------------------------------- |
| `name`        | Recipe name                                                |
| `id`          | Recipe ID                                                  |
| `tags`        | Food.com tags for recipe                                   |
| `rating`      | Rating given                                               |
| `calories`    | Calories per serving                                       |
| `total_fat`   | Total fat (percentage of daily value)                      |
| `sugar`       | Sugar (percentage of daily value)                          |
| `sodium`      | Sodium (percentage of daily value)                         |
| `protein`     | Protein (percentage of daily value)                        |
| `saturated_fat` | Saturated fat (percentage of daily value)                |
| `avg_rating`  | Average rating per recipe                                  |
| `has_veggies` | Boolean indicator if recipe has 'vegetables' tag           |
| `is_healthy`  | Boolean indicator if recipe has 'healthy' tag              |



This is the first few rows of my cleaned dataset:

| name                                 |     id | tags                                                                                                                                                                                                                        |   rating |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   avg_rating |   has_veggies |   is_healthy |
|:-------------------------------------|-------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------:|-----------:|------------:|--------:|---------:|----------:|----------------:|-------------:|--------------:|-------------:|
| 1 brownies in the world    best ever | 333281 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings'] |        4 |      138.4 |          10 |      50 |        3 |         3 |              19 |            4 |             0 |            0 |
| 1 in canada chocolate chip cookies   | 453467 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                               |        5 |      595.1 |          46 |     211 |       22 |        13 |              51 |            5 |             0 |            0 |
| 412 broccoli casserole               | 306168 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |        5 |      194.8 |          20 |       6 |       32 |        22 |              36 |            5 |             1 |            0 |
| 412 broccoli casserole               | 306168 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |        5 |      194.8 |          20 |       6 |       32 |        22 |              36 |            5 |             1 |            0 |
| 412 broccoli casserole               | 306168 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                        |        5 |      194.8 |          20 |       6 |       32 |        22 |              36 |            5 |             1 |            0 |



### Univariate Analysis

Here is a plot that displays the distribution of average recipe ratings:

<iframe src="assets/univariate.html" width="650" height="400" frameborder="0" ></iframe>

The histogram shows the distribution of average recipe ratings. Most recipes have an average rating of 4 or higher, indicating that users generally rate recipes quite positively. The mode of the distribution is at a rating of 5, suggesting that a significant number of recipes receive the highest possible rating.

### Bivariate Analysis

Here is a plot that displays the relationship between calories and average ratings:

<iframe src="assets/bivar_cals.html" width="650" height="400" frameborder="0" ></iframe> 

The scatter plot illustrates the relationship between the number of calories and the average ratings of recipes. While there is some spread in the data, there does not appear to be a strong correlation between calories and average ratings. Recipes with a wide range of calorie content can still achieve high ratings, suggesting that factors other than calorie count may play a more significant role in user ratings.

### Interesting Aggregates
<!-- TODO -->

## Assessment of Missingness

One of the columns in the dataset with significant missing values is the `rating` column. Another is the `description` column. In this section we will be exploring the missingness in the data.

### NMAR Analysis

Descriptions are often provided when the contributor has something notable or specific to say about the recipe. If contributors feel that the recipe is self-explanatory, straightforward, or lacks unique characteristics, they might omit the description. This decision is influenced by the contributor's subjective judgment, making the missingness dependent on the complexity and the nature of the recipe.

### Missingness Dependency

We conducted permutation tests to evaluate whether the missingness in the avg_rating column depends on the `calories` and `sodium` columns in our dataset. The permutation tests simulate the null hypothesis that there is no relationship between the missingness in avg_rating and the respective column by randomly shuffling the data and recalculating the test statistic.


**Testing Dependency on calories:**

**Null Hypothesis:** The missingness of `avg_rating` does not depend on `calories`.

**Alternative Hypothesis:** The missingness of `avg_rating` depends on `calories`.

**Test Statistic:** Absolute difference in mean `calories` between groups with and without missing `avg_rating`.

**Results:** Observed Difference: 102.607, P-value: 0.0

The histogram below shows the empirical distribution of the test statistic for the permutation test on calories. The observed statistic is marked with a red dashed line. The observed difference falls outside the bulk of the permutation differences, suggesting that there is a significant dependency of the missingness of avg_rating on the calories column.

<iframe src="assets/cal_missing.html" width="650" height="400" frameborder="0" ></iframe>

**Testing Dependency on sodium:**

**Null Hypothesis:** The missingness of `avg_rating` does not depend on `sodium`.

**Alternative Hypothesis:** The missingness of `avg_rating` depends on `sodium`.

**Test Statistic:** Absolute difference in mean `sodium` between groups with and without missing `avg_rating`.

**Results:** Observed Difference: -0.232, P-value: 0.903

The histogram below shows the empirical distribution of the test statistic under the null hypothesis. The observed difference, marked by the red dashed line, lies well within the bulk of the null distribution, suggesting no significant dependency between the missingness in avg_rating and the sodium column. Therefore, we fail to reject the null hypothesis for sodium.

<iframe src="assets/sodium_missing.html" width="650" height="400" frameborder="0" ></iframe>

**Based on the results of the permutation tests:**
The missingness in `avg_rating` is significantly dependent on `calories` however, there was no significant dependency between the missingness in `avg_rating` and `sodium`.


## Hypothesis Testing
<!-- TODO -->

## Framing a Prediction Problem

Our goal is to predict the average rating (`avg_rating`) of recipes based on their attributes, making this a regression problem as `avg_rating` is a continuous variable. By accurately forecasting `avg_rating`, which directly measures a recipe's perceived quality and popularity among users, we can determine which attributes influence user preferences. This understanding allows recipe creators to tailor their offerings to better meet user expectations and improve overall satisfaction.

To evaluate our model, we use Mean Squared Error (MSE) as the primary metric, along with R-squared and Mean Absolute Error (MAE) for additional insights. MSE is preferred because it is more sensitive to larger errors, making it effective for identifying models with significant prediction inaccuracies. R-squared provides a measure of how well the model explains the variability of the response data, and MAE offers an easily interpretable magnitude of errors. Together, these metrics give a well-rounded assessment of our model's prediction accuracy.

Our baseline model uses three features: `sodium`, `is_healthy`, and `has_veggies`. These features are relevant and available at the time of prediction, ensuring our model's validity. In the final model, we incorporate additional features, including saturated_fat and a calculated health_score based on thresholds for `sodium`, `sugar`, `protein`, and `calorie` content. These features are known beforehand and do not rely on any future information.

By integrating these improved features and fine-tuning the hyperparameters for a Random Forest Regressor, the final model can better capture the complex interactions between recipe attributes. This approach leads to more accurate predictions of user ratings. The progression from a simple to a more sophisticated model highlights how incorporating meaningful features and advanced techniques can significantly enhance predictive performance in real-world scenarios.

## Baseline Model

The baseline model predicts a recipe's average rating (`avg_rating`) using three features: `sodium`, `is_healthy`, and `has_veggies`. Among these, `sodium` is a quantitative variable representing the amount of `sodium` in a recipe. The other two, `is_healthy` and `has_veggies`, are nominal variables indicating whether a recipe has the tag 'healthy' and whether it has the tag 'vegetables', respectively. To encode the nominal variables, we used a OneHotEncoder as part of a ColumnTransformer. This ensures that the categorical variables are transformed into binary indicator variables suitable for regression modeling.

The model's performance metrics are as follows:
- Mean Squared Error (MSE): 0.2396
- R-squared: 0.0017
- Mean Absolute Error (MAE): 0.3397

Based on these metrics, the baseline model has limited predictive power, as indicated by the low R-squared value. This suggests that the model does not explain much of the variability in the average ratings. While the baseline model provides a foundation, its performance indicates there is significant room for improvement.

## Final Model

To enhance the model, we added the following features:
1. **Saturated Fat** (`saturated_fat`): A quantitative measure of fat content, which could influence health-conscious users' perceptions of a recipe.
2. **Health Score** (`health_score`): A composite score calculated using binary indicators for low sodium, low sugar, high protein, and low calorie content. This feature summarises multiple health-related aspects into a single variable that could strongly correlate with user preferences.

These additional features are well-suited to the prediction task because they capture more nuanced health and nutritional factors that likely affect user ratings. For example, recipes with balanced health scores may appeal to a broader audience, directly influencing their average ratings.

The final model uses a Random Forest Regressor, a flexible and robust algorithm capable of capturing complex feature interactions and nonlinear relationships. We tuned hyperparameters using a Grid Search with 3-fold cross-validation to find the best combination of:
- `n_estimators` (50, 100), controlling the number of trees in the forest.
- `max_depth` (None, 10, 20), limiting the depth of individual trees to avoid overfitting.

The final model's performance metrics improved significantly over the baseline:
- Mean Squared Error (MSE): 0.1955
- R-squared: 0.1856
- Mean Absolute Error (MAE): 0.2542

These improvements in performance metrics, particularly the higher R-squared value, indicate that the final model better captures the variability in average ratings. This enhancement is likely due to the inclusion of more informative features and the implementation of the Random Forest Regressor algorithm. The final model's ability to account for complex interactions between variables has resulted in more accurate predictions. However, while there is a noticeable improvement, the overall metrics still suggest that the model is not exceptionally strong. This observation potentially implies that the average rating of a recipe is not predominantly influenced by its nutritional factors alone. Additional aspects, such as taste, ease of preparation, and user experience, might play a more significant role in determining the overall ratings.

## Fairness Analysis





