# Project 625: Prediction of the risk of a Myocardial Infarction or Heart Attack using different Machine Learning 


## preprocessing
- Missing data
1. we select variables with low rate of missing data(<20%), and then we get a dataset with 296320 observations of 83 variables.

2. Due to our binary outcome which is a Myocardial Infarction or Heart Attack(C15CCMI), we delete observations with missing value in this column.

3. we choose the eligiable repondents based on "SAMPLED" and "SFLAG" columns, then we delete three columns named "COHORT","SAMPLED","R15SRVDISP","R15SRVMODE","P15PLREGCDE" and "SFLAG".(we only use baseline information and delete the "COHORT" column where the values are totally same) Thus, we get the dataset named "ori_data.csv" with 296320 obseravtions of 77 variables.

4. do imputation using mice function with 5 iterations. Then, we get the "completed_data.csv" file.

## Feature Selection
After deleting the ID column, we have 75+1 features for now in 'completed_data.csv'. First we define most of them are categorical variables and we convert them to factor. Thus, it is more likely to be overfitting when we do Machine Learning Models.

- the structure of the dataset

![Screenshot 2023-11-30 115513](https://github.com/sangyisu/625-project/assets/117102360/888bd7cd-02c4-45be-a0b3-840ee4b6fb7f)

  
- Methods for feature selection
1. pearson correlation
2. chi-suquared test
3. 
