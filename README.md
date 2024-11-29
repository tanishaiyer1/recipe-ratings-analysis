# Analysis of Average Recipe Ratings
**By: Tanisha Iyer and Reva Agrawal**

## Introduction 
Whether we are cooking dinner at home or looking up recipes for special occasions, everyone has their go-to favorites and opinions about what makes a dish great. Our health is really important and recently, more people have been paying attention to the nutritional value of the food they consume. The central question of our project is: **"Do the nutritional factors of a recipe have an impact on the average rating given to that recipe?"** This question is crucial because it helps us understand how health-conscious choices impact culinary preferences and ratings, offering valuable insights for both consumers and recipe creators.

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
We first had to clean the raw data. We started by merging the two datasets on id and recipe_id. We then handled all missing rating by replacing all zero ratings with NaN values. Next we Converted the nutrition column from a string representation of a list to individual numerical columns for each nutrient and then removed the original nutrition column. We also calculated the average rating for each recipe and added it as a new column. Next we added binary indicators for the presence of vegetables (has_veggies) and whether the recipe is tagged as healthy (is_healthy). Finally, we identified and removed duplicate entries based on the recipe ID to avoid redundant analyses. Our analysis is focused on the avg_rating column so removing the duplicate id's doesn't loose any relevant data.

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

| name                                 |     id | tags                                                                                                                                                                                                                                                                                               |   rating |   calories |   total_fat |   sugar |   sodium |   protein |   saturated_fat |   avg_rating |   has_veggies |   is_healthy |
|:-------------------------------------|-------:|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------:|-----------:|------------:|--------:|---------:|----------:|----------------:|-------------:|--------------:|-------------:|
| 1 brownies in the world    best ever | 333281 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                        |        4 |      138.4 |          10 |      50 |        3 |         3 |              19 |            4 |             0 |            0 |
| 1 in canada chocolate chip cookies   | 453467 | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                      |        5 |      595.1 |          46 |     211 |       22 |        13 |              51 |            5 |             0 |            0 |
| 412 broccoli casserole               | 306168 | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                               |        5 |      194.8 |          20 |       6 |       32 |        22 |              36 |            5 |             1 |            0 |
| millionaire pound cake               | 286009 | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] |        5 |      878.3 |          63 |     326 |       13 |        20 |             123 |            5 |             0 |            0 |
| 2000 meatloaf                        | 475785 | ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                             |        5 |      267   |          30 |      12 |       12 |        29 |              48 |            5 |             1 |            0 |


### Univariate Analysis
Here is a plot that displays the distribution of average recipe ratings:
<iframe src="/Users/tanishaiyer/Documents/DSC/recipe-ratings-analysis/assets/univariate.html" width="800" height="600" frameborder="0" ></iframe>

The histogram shows the distribution of average recipe ratings. Most recipes have an average rating of 4 or higher, indicating that users generally rate recipes quite positively. The mode of the distribution is at a rating of 5, suggesting that a significant number of recipes receive the highest possible rating.



### Bivariate Analysis
Here is a plot that displays the relationship between calories and average ratings:

The scatter plot illustrates the relationship between the number of calories and the average ratings of recipes. While there is some spread in the data, there does not appear to be a strong correlation between calories and average ratings. Recipes with a wide range of calorie content can still achieve high ratings, suggesting that factors other than calorie count may play a more significant role in user ratings.







