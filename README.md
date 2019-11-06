
# Project 2 - Ames Housing Data and Kaggle Challenge
Readme by Kristina Joos

Structure:
Structure of code:

Notebook 1: Cleaning and Modifications of Train Data and EDA.  
Notebook 2: Cleaning and Modifications of Test Data.  
Notebook 3: Creation of the Null Treatment Data Frame.  
Notebook 4: Modeling.  

---

Goal
---

I am going to use the Ames Housing Data to build a model that predicts unknown house prices for a house with given features. For this model, I am going to use different features from the data set and deploy a linear regression algorithm to find a model that accurately predicts the house prices and is easy to implement.

EDA
---

The data set contains information from the Ames Assessor's Office used in computing assessed values for individual residential properties sold in Ames, IA, from 2006 to 2010.
It has 2980 rows (houses) and 82 columns (features).
There are a lot of very detailed house features listed in the data set: quality of material and finish of the house, number of bathrooms, roof material, and many more. The average sale price of the houses is $181469.

Handling Null Values
---

A lot of columns have a large amount of null values. 
To get an overview of columns that contain null values, I created a data frame that contains information about the columns that contain null values and added how I am going to treat these columns. 
The null value data frame can be found in Notebook 3.
Taking the feature description into consideration, I filled a lot of null values with 0: In many columns the NaN values in the data frame are synonymous with the feature not being present in the house.
For lot_frontage (Linear feet of street connected to the property), I filled NaN values with median lot frontage in the neighborhood.

Dummy Variables
---

From the columns that had an object data type, I selected a couple of columns that seem to be essential for predicting a house price and turned them into dummies: neighborhood, bldg_type, house_style, heating, central_air, garage_type, utilities.


Feature Engineering
---

I engeniert the following features out of highly correlated features:
'total_liv_sqft', 'total_bsmt_1st_flr_sf','garage_total'.

Dropping outliers
---

For two houses, the total living space area was very high, and their sales price very low.
I dropped those two houses from the data set.

Sale Price distribution
---

The distribution for the sale prices is right-skewed.
After transforming sale price using the natural logarithm, the distribution looks gaussian.
I decided to use log(saleprice) for modeling.

Selecting Features
---

I looked at the correlations between features and sales price.
For my first feature set, I selected all the features that have a correlation coefficient bigger than 0.5 with the sales price.

Modeling
---

For the modeling, I wrote a class to automate the model building and prediction.

I ran linear regressions without regularization on different, with sale price correlated features.
I used LASSO, Ridge, and Elastic Net regression on a broader set of features.
The best performing models are those with more features and a regularized linear regression.


Conclusion
---

Prudent feature selection didn't work very well for me. The R2 score was okay, but not great (<0.89), and many carefully selected features had low probability of influencing the model.

Using many features and a regularization method produced the best models.

It would be interesting to incorporate location (more than just the neighborhood ) into the models. Prices within a neighborhood vary, and a feature that more closely describes the location (e.g. coordinates) would be helpful.

For a production model, I would choose a model with easily accessible features that are known for most houses.
For many houses, very detailed information (e.g. the sqft of the siding) might not be available.

