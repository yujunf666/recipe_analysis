# recipe_analysis
This is a project for DSC80 at UCSD.
## Introduction
In modern times, as cities expand and lifestyles accelerate, individuals face higher stress levels. Research shows that this stress often leads to a preference for high-calorie foods, which are believed to stimulate dopamine production and foster a sense of well-being. However, this dietary choice often comes with health risks.

We will explore the relationship between the complexity of recipes (expressed as number of ingredients) and the public acceptance and nutritional value of these meals. By studying this relationship, we aimed to reveal whether simpler or more complex recipes are preferred. Additionally, we will reveal the composition of different foods in relation to their calories. We think research like this can help people make healthier lifestyle choices.

### Introduction to the Datasets in this Study
Our first dataset comprises details from 83,782 recipes on food.com. It includes 10 columns with various information related to these recipes:

|Column	                 |Description|
|---                     |---        |
|`'name'	`            |Recipe name|
|`'id'`	                 |Recipe ID|
|`'minutes'`	         |Minutes to prepare recipe|
|`'contributor_id'`	     |User ID who submitted this recipe|
|`'submitted'`	            | Date recipe was submitted|
|`'tags'`	              |Food.com tags for recipe|
|`'nutrition'`	          |Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein    (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”|
|`'n_steps'`	          |Number of steps in recipe|
|`'steps'`	              |Text for recipe steps, in order|
|`'description'`	     | User-provided description|

The second dataset contains 731,927 reviews from users regarding recipes on food.com, organized into five distinct columns.

|Column|Description|
|---|---|
|`'user_id'`	|User ID|
|`'recipe_id'`	|Recipe ID|
|`'date'`	|Date of interaction|
|`'rating'`	|Rating given|
|`'review'`	|Review text|

In our study, we mainly used the "nutrition", "n_ingredients", and "rating" columns. These three columns contain important information needed for our research problem.

---
## Cleaning Data and Exploratory Data Analysis
### Data Cleaning
To simplify our data analysis and integration process, we executed the following data cleaning steps:

1. **Merging Recipe and Review Datasets (Left Merge)**: We combined the recipe and review datasets into a single dataframe to align comments with their respective recipes, facilitating easier comparison.
2. **Replacing 0 Ratings with N/A**: This step is crucial for data cleansing as ratings of 0 typically signal missing values. This stems from the fact that on most rating platforms, the minimum possible score is 1, not 0. Hence, a 0 rating is likely the result of automated fill-ins for absent ratings.
3. **Adjusting Column Data Types**: We corrected the data types of various columns to enhance accuracy; for example, transforming date and submitted into DateTime formats, minutes into float, and n_steps and n_ingredients into integers.
4. **Figure out the average rating per recipe**: We calculated the average rating for each recipe based on its reviews and ratings. Then, we used the merge method to append this series back to the main dataframe. This makes it easy for us to see people’s comprehensive reviews of different recipes.
5. **Subdivide the nutrition column**: We subdivide the "nutrition" column into the following columns: calories, total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV). Through this step, we can directly access these columns when studying the relationship between nutrition and calories.
6. **Division of difficulty ratings**: Based on the number of steps in different recipes, we divide the difficulty of the recipes into several levels. This step facilitates our analysis of Interesting Aggregates.

After these cleaning steps, the cleaned dataframe looked like this:

| calories | total fat (PDV) | sugar (PDV) | sodium (PDV) | protein (PDV) | saturated fat (PDV) | carbohydrates (PDV) |
|----------|-----------------|-------------|--------------|---------------|---------------------|---------------------|
| 138.4    | 10              | 50          | 3            | 3             | 19                  | 6                   |
| 595.1    | 46              | 211         | 22           | 13            | 51                  | 26                  |
| 194.8    | 20              | 6           | 32           | 22            | 36                  | 3                   |
| 194.8    | 20              | 6           | 32           | 22            | 36                  | 3                   |
| 194.8    | 20              | 6           | 32           | 22            | 36                  | 3                   |

Note: This only showing the first 5 rows and last few columns for illustration, the actual cleaned dataframe is of 234429 rows × 27 columns

### Univariate Analysis
We mainly looked at the overall distribution of number of ingredients.
#### Distribution of Number of Ingredients
From the histogram below, we found that most recipes contain between 5 to 10 ingredients, with the frequency decreasing as the number of ingredients increases, indicating that simpler recipes with fewer ingredients are more common.

<iframe
  src="assets/fig_2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### Bivariate Analysis
To determine if there's a relationship between two variables, it's crucial to examine how they interact with each other. In this section, we'll employ a scatter plot to visually represent the connection between a recipe's ingredient count and its ratings.

The plot suggests a lack of strong correlation between the number of ingredients and the recipe ratings, as ratings remain relatively consistent across a varying number of ingredients.

<iframe
  src="assets/fig_4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Interesting Aggregates
Currently, we employ a scatter plot to explore the relationship between the number of ingredients and recipe ratings. However, considering the potential link between the number of ingredients and the number of steps in a recipe (with the assumption that more steps might involve the addition of more ingredients), we have decided to utilize a pivot table for a more in-depth analysis of the possible connections among the number of steps, number of ingredients, ratings, and calorie content.

In the steps of Data Celaning, we rated the difficulty of making different recipes based on the value of n_steps. Based on this Pivot Table, we found that as the difficulty increases, calories and n_ingredients show an increasing trend, while the changes in ratings are not obvious. This is partially in line with our previous guess.

| diff_level   |   calories |   n_ingredients |   rating |
|:-------------|-----------:|----------------:|---------:|
| Easy         |    332.272 |         7.16592 |  4.68805 |
| Med_1        |    411.129 |         9.11379 |  4.67035 |
| Med_2        |    487.115 |        10.7553  |  4.68268 |
| Med_3        |    621.919 |        12.0205  |  4.69694 |
| Hard         |    676.357 |        13.0796  |  4.681   |


---
## Assessment of Missingness
### NMAR Analysis
One of the column in our dataset with missing values that is possibly NMAR is the `rating` column. If the ratings were np.nan because users chose not to rate (possibly due to dissatisfaction or indifference), and this lack of rating was represented by np.nan, then the data could be considered NMAR.

However, with additional info could be got from the "review" column, if users failed to make the recipe, they might not rate and leave a failed message in the review area, so in this case, ratings might be MAR.

### Missingness Dependency


---
## Hypothesis Testing

The research question we aim to investigate is whether recipes containing a variety of ingredients are rated on the same scale as those with simpler ingredients.

For the purpose of this study, we will classify a recipe as containing diverse ingredients if it consists of ten or more components. Our analysis will involve conducting a permutation test.

### Setting Up the Testing

Null Hypothesis H0: People tend to give recipes with more ingredients the same ratings.

Alternative Hypothesis H1: People tend to give recipes with more ingredients higher ratings.

We would select only the useful columns, including n_ingredients and average rating, and also create new column named `diverse`, which is true if it has steps larger than or eqaul to 10 and false if has steps less 10.

|   | n_ingredients |   ave_rating | diverse   |
|--:|--------------:|-------------:|:----------|
| 0 |         9     |            4 | False     |
| 1 |        11     |            5 | True      |
| 2 |         9     |            5 | False     |
| 3 |         9     |            5 | False     |
| 4 |         9     |            5 | False     |

The reason for choosing one-sided test is that we would assume more ingredients often mean a greater variety of flavors and textures, which can create a more complex and satisfying taste experience, so people would give higher rating for recipes with diverse ingredients.

| complex   |   n_steps |   ave_rating |
|:----------|----------:|-------------:|
| False     |   6.52479 |      4.68135 |
| True      |  12.73752 |      4.67771 |

Given that "ave_rating" is numerical data, it is appropriate to utilize the difference in means as the test statistic. In our research, we will set the significance level to `0.05`

The observed difference in mean is `0.00364915`

### Hypothesis Testing Conclusion

We ran permutation test for 1000 times. The P-value for the testing is 0.118, which means that at significant level of 0.05, we are unable to reject the null hypothesis.

This result could be reasonable, since though recipes with more ingredients may offer us a more complex and satisfying taste experience, more ingredients mean our preparation work becomes more complex, and some people may find it troublesome and therefore not rate the recipe highly. This tradeoff might make the number of ingredients statistically unsignificant in average rating of recipes.


---
## Framing a Prediction Problem

We will predict the "calories" of a recipe, which makes this a regression problem since calories are a  numerical continuous variable. The "calories" column is chosen as the response variable because it represents an important aspect of dietary information that many people consider when selecting a recipe. It is a quantifiable attribute that can significantly impact health and nutrition choices.

For evaluating our regression model, we can use the Coefficient of Determination(R Squared) and Root Mean Squared Error (RMSE)

**R^2** is chosen because it represents the proportion of the variance in the dependent variable that is predictable from the independent variables. It gives a sense of the goodness of fit of our model. An R² value closer to 1 indicates that our model explains a high proportion of the variance in calorie data, making it a valuable metric for assessing the performance of our model in terms of explanatory power.

**RMSE** is useful as it gives more weight to larger errors (due to the squaring part), which can be beneficial if larger errors are particularly undesirable in our context. RMSE is chosen over metrics like Mean Squared Error (MSE) when large errors are not particularly more critical than smaller ones, ensuring a more even-handed evaluation. 

- Features to be considered must be known before a recipe is actually tried and its calories are determined. Suitable features might include:
  - Recipe ingredients (columns such as "total fat (PDV)")
  - Preparation time ('minutes')
  - Number of steps ('n_steps')
  - Tags associated with the recipe ('tags')
- We should not use features that would only be known after the recipe's calories are determined, such as the reviews ('review') or the average rating ('avg_rating'), as these may be influenced by the outcome (calories) and would not be available at the time of prediction.


---
<iframe
  src="assets/fig_1.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig_2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig_3.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
<iframe
  src="assets/fig_4.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
