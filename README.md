# Project 625: Prediction of the risk of a Myocardial Infarction or Heart Attack using different Machine Learning 


## preprocessing
- Missing data
1. we select variables with low rate of missing data(<20%), and then we get a dataset with 296320 observations of 83 variables.

2. Due to our binary outcome which is a Myocardial Infarction or Heart Attack(C15CCMI), we delete observations with missing value in this column.

3. we choose the eligiable repondents based on "SAMPLED" and "SFLAG" columns, then we delete three columns named "COHORT","SAMPLED" and "SFLAG".(we only use baseline data and delete the "COHORT" column where the values are totally same) Thus, we get the dataset named "ori_data.csv" with 125548 obseravtions of 80 variables.

4. do imputation using mice function with 5 iterations. Then, we get the "completed_data.csv" file.
