# About the Data

link: https://www.kaggle.com/arashnic/hr-analytics-job-change-of-data-scientists

A company which is active in Big Data and Data Science wants to hire data scientists among people who successfully pass some courses which conduct 
by the company. Many people signup for their training. Company wants to know which of these candidates are really wants to work for the company after 
training or looking for a new employment because it helps to reduce the cost and time as well as the quality of training or planning the courses and 
categorization of candidates. Information related to demographics, education, experience are in hands from candidates signup and enrollment.

This dataset designed to understand the factors that lead a person to leave current job for HR researches too. By model(s) that uses the current 
credentials,demographics,experience data you will predict the probability of a candidate to look for a new job or will work for the company, as well 
as interpreting affected factors on employee decision.

# Missing Data

Missing values occur in all kinds of datasets from industry to academia. They can be represented differently - sometimes by a question mark, or -999, sometimes by 'n/a', or by some other dedicated number or character.

Detecting and handling missing values in the correct way is important, as they can impact the result of the analysis, and there are algorithms that can't handle them.

There is no penancea for all missing value imputation problems. For example, if missing values are due to a malfunctioning of the measuring machine and therefore real numerical values are just not recorded then in that case you can't impute missing values with 0 whereas if missing values appear where there is nothing to measure then it can be imputed by 0.

Some methods of detecting missing values and of which type:
- Histograms are a great tool to find placeholder character, if any.
- Usually, for nominal data, it is easier to recognise the placeholder for missing values, since the string format allows is to write some reference to a missing value, like 'unknown' or 'n/a'.

Missing values are usually classified into three different types:

1. Missing Completely at Random (MCAR): The probability of an instance being missing does not depend on known values or the missing value itself. Here we can assume that the missing values follow the same distribution as the known values.
2. Missing at Random (MAR): The probability of an instance being missing may depend on known values but not on the missing value itself.
3. Not Missing at Random (NMAR): The probability of an instance missing may depend on the value of variable itself.

Only knowledge of the data collection process and the business experience can tell whether the missing values we have found are of type MCAR, MAR or NMAR.

Imputing NMAR missing values is more complicated, since additional factors to just statistical distribution and statistical parameters have to be taken into account.

# Data Imputation

Data imputation is a method in which the missing values in any variable or dataset are filled with numeric values for performing the task.

There can be various reasons for imputing data, many real-world datasets containing missing values which can be in any form such as blanks, NaN, 0s, any categorical symbol. Instead of just dropping the rows or columns containing the missing values, which come at the price of losing data that may be valuable, a better strategy is to blame the missing values.

Removing rows is a good option when missing values are rare. But this is not always practical.

There are many options to pick from when replacing a missing value:
1. A single pre-decided constant value, such as 0.
2. Taking value from another randomly selected sample.
3. Mean, median or mode for the column.
4. Interpolate value using a predictive model or algorithm.

# Handling Missing Values

## Deletion Methods

There are three common deletion:
1. Likewise Deletion: Delete all rows where one or more values are missing.
2. Pairwise Deletion: Delete only the rows that have missing values in the columns used for the analysis.
3. Dropping Features: Drop entire columns with more missing values than a given threshold, for example 60%.

## Simple Imputer

SimpleImputer is used for imputations on univariate datasets. It allows us to attribute values in any feature column using only missing values in that feature space.

Different strategies are provided to attribute data, such as crediting with a constant value or using statistical methods such as mean, median or mode to attribute data for each missing value column.

It supports the 'most-frequent' strategy, which is like the mode of numerical values for categorical data representations.

## Multiple Imputation by Chained Equation (MICE)

Multiple imputation is a process where the misisng vlaues are filled multiple times to create 'complete' datasets.

Multiple imputation has a lot of advantages over traditional single imputation methods.

MICE is an imputtaion method that works with the assumption that the missing data is missing at random (MAR) that is the nature of missing data is related to the the observed data but not the missing data.

MICE algorithm woks by running multiple regression models and each misisng value is modeled conditionally depending on the observed (non-missing) values.

MICE Steps:
1. A simple imputation, such as imputing the mean, is performed for every misisng value in the dataset. These imputations can be thought of as 'place holders'.
2. The 'place holder' mean imputations for one variable 'var' are set to missing.
3. The observed values from the variable 'var' in step 2 are regressed on the other variables in the imputation model, which may or may not consist of all of the other variables in the dataset. In other words, 'var' is the dependent variable in a regression model and all the other variables are independent variables in the regression model.
4. The missing values for 'var' are then replaced with predictions from the regression model. The 'var' is subsequently used as an independent variable in the regression models for other variables, both the observed and these imputed values will be used.
5. Step 2-4 are then repeated for each variable that has missing data. The cycling through each of the variables constitutes one ineteration or 'cycle'. At the end of one cycle all of the missing values have been replaced with predictions from regressions that reflect the relationships observed in the data.
6. Steps 2-5 are repeted for a number of cycles. with the imputations being updated at each cycle.

## KNN Imputer

KnnImputer is a multivariate data imputation technique used for filling missing data using the K-Nearest Neighbors approach. The mean value fills each missing value from the neighbors found in the training set, either weighted or unweighted.

If the sample has more than one feature missing, then neigbors for that sample can be different. If the number of neighbors are lesser than n_neighbors specified, there is no defined distance in the training set. The average of that training set is used during imputation.

Nearest Neighbors are selected based on distance metrics, by default, it is set to euclidean distance and n_neighbor is specified to consider for each step.

The main disadvantage of using KNN Imputation is that it becomes time-consuming when analysing large datasets as it searches for similar instances through all the dataset. Also choosing the correct value for k (n_neighbor) is an important factor.

## Miss Forest

It is another technique used to fill in the missing values using random forest in an iterated fashion.

Miss Forest Steps:
1. The candidate column is selected from all the columns having the least number of missing values.
2. In the next step, all the other columns, ie non-candidate columns having missing values, are filled with the mean for the numerical columns and categorical columns.
3. After that, imputer fits a random forest model with the candidate column as the outcome variable (target variable) and remaining columns as independent variables and then filling the missing values in the candidate column using the predictions from the fitted Random Forest model.
4. Then the imputer moves on, and the next candidate column is selected with the second least number of missing values, and the process repeat itself for each column with the missing values.

# Summary

Our dataset has a lot of features that are categorical (Nominal, Ordinal, Binary), some with high cardinality. After applying the above mentioned techniques, these are our observations:

1. The model was giving a good AUC score with the SimpleImputer technique.
2. The performace of the models showed improvement specially on CatBoost after using the above mentioned data imputation techniques.
3. Miss Forest showed the best performance with a significant boost of AUC score.






