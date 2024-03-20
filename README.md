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
>>>>>>> 66fd859 (changed title of website)
