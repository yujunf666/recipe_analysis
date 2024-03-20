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