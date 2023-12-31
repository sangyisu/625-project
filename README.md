# Project 625: Prediction of the risk of a Myocardial Infarction or Heart Attack using different Machine Learning 


## File
625finalcodes.rmd :  all code

final report : report 

ori_data : raw data

imputed data ("mice_data29w.csv" ) :  https://drive.google.com/file/d/1T7QF7F4SpDmfhVjIjrw2iwED_rjfdsoC/view?usp=drive_link


## Challenges
1. The significant challenge of handling a large and complex dataset.
2. The Multivariate Imputation by Chained Equations (MICE) function, particularly using the Predictive Mean Matching (PMM) method, struggled with the multi-type nature of our data.
3. The dataset was too large for imputation using mice and the imputation process was extremely slow.
4. The imputation for each machine learning model was also time-consuming.
5. We used cluster in "Biostat" and "Great Lakes" to run the parallel processes.

## Preprocessing
- Establish dataset

We select the columns with "C15" in names. Thus we get the dataset with information of 2012 survey. And the dataset includes 296320 observations of 88 variables.

- Missing data

1. Select variables with low rate of missing data(<20%), and then we get a dataset with 296320 observations of 81 variables.

To refine the dataset for more effective analysis, variables with over 20% missing data were omitted, leading to a more manageable set of 296,320 entries across 81 variables.

2. Delete ID and COHORT columns. (81-2 = 79)

ID and Cohort columns are removed.

3. Do imputation using mice function with 1 iterations. Then, we get the "mice_data.csv" file. The dataset includes 296320 observations of 79 variables.

To solve the problem of low speed, parallel processing and data separating functions were adopted using the multi-core capabilities of the Great Lakes cluster. The core strategy involved the use of the 'foreach' function to simultaneously execute the imputation functions across multiple cores. Then the results from each processing unit were combined into a single, cohesive dataset. This approach improved the speed and overall effectiveness of our data imputation.


## Feature Selection

 We have 79 features for now in 'mice_data29w.csv'. First we define most of them are categorical variables and we convert them to factor. Thus, it is more likely to be overfitting when we do Machine Learning Models.


- The types of Variables(79)

1.Boolean Variables: "BMICAT"(if obese) "MRSTAT"(if married) "C15READ""C15HEAR""C15CCHBP""C15CC_CAD""C15CC_CHF""C15CCMI""C15CCHRTOTH" "C15CCSTROKE" "C15CC_COPD"  "C15CCGI"     "C15CCARTHIP" "C15CCARTHND" "C15CCOSTEO"  "C15CCSCIATI" "C15CCDIABET" "C15CCANYCA"  "C15DEP2WK"  "C15DEPYR"    "C15DEP2YR"   "C15MUILKG"   "C15PAOADV"   "C15FRMFALL" "C15FRMBAL"   "C15OTOTEST"

2.Oridinal Variables: "AGE"  "EDUC" 

3.Nominal Variables: "GENDER" "RACE" "C15VRGENHTH" "C15VRMACT"   "C15VRSTAIR"  "C15VRPACCL"  "C15VRPWORK"  "C15VRMACCL"  "C15VRMWORK"  "C15VRPAIN"  "C15VRCALM"   "C15VRENERGY" "C15VRDOWN"   "C15VRSACT"  "C15VRPHCMP"  "C15VRMHCMP"  "C15ADLBTH"   "C15ADLDRS"   "C15ADLEAT"  "C15ADLCHR"   "C15ADLWLK"   "C15ADLTLT"     "C15CHSTEX"   "C15CHSTRST"  "C15SOBFLT"   "C15SOBSIT"   "C15SOBWLK"   "C15SOBSTR"   "C15FTNUMB"   "C15FTSENS"   "C15FTHC"  "C15FTSRS"    "C15PNART"    "C15PNBACK"   "C15DEPWEEK"  "C15CMPHTH"  "C15SMOKE"    "C15PAOTLK"   "C15FRMTLK"   "C15FRMPREV"  "C15CMPWHO"  "C15SRVDISP"  "C15SRVMODE"    "C15SRVLANG" 

4. Continuous(number): "C15HDACT" "C15HDPHY" "C15HDMEN"  "C15PCTCMP" (4)

![Screenshot 2023-11-30 121957](https://github.com/sangyisu/625-project/assets/117102360/6ca97866-a7d7-478a-9369-cf5e2ed15306)

  
- Methods for feature selection
1. Chi-Suquared Feature Selection
   Use pair-wise chi-squared test, and we only delete one column named “C15PAOTLK” (p=0.1869).
   
![table1](https://github.com/sangyisu/625-project/assets/117102360/9048296e-8b7b-469c-9894-04b66f916ced)


## Machine Learning Models

Model Built Using Mutual Information Features

- Logistic regression

- Support Vector Method

For this model, the training data comprises a randomly selected subset of 10,000
observations from the large training dataset, while the test data consists of 4,200 observations from the large
testing dataset. In the case of support vector machines, the cost value is carefully adjusted through tuning,
and the best-performing cost value is found to be 15.

![figure1](https://github.com/sangyisu/625-project/assets/117102360/f35df227-9671-4c85-b326-55c9ea54a3d0)


- Naive Bayes
  
For our study, we fine-tuned the Laplace parameter of Naive Bayes and found that a value of 0 was optimal (Figure 2). This adjustment enhanced the accuracy of our results.
![figure2](https://github.com/sangyisu/625-project/assets/117102360/9ecbe924-a06d-46db-8aff-88f3ba8f3a71)

- Random Forest
  
In our study, the ‘ntree’ (number of trees) and ‘mtry’ (number of features tried at each split) parameters were adjusted meticulously within the Random Forest model. The optimal configuration is ntree
= 300 and mtry =8.831761.

![figure3](https://github.com/sangyisu/625-project/assets/117102360/7de1dfbe-62ed-4925-8cb1-e64939685092)

![figure4](https://github.com/sangyisu/625-project/assets/117102360/c0a89268-f57b-468f-a152-f4807c3f7b26)

- Decision Tree
  
The Decision Tree model operates like a tree structure, making decisions at each node based on a feature, leading to further nodes or outcomes (leaves). This model uses recursive dataset splitting for decision-making, known for its interpretability and visual clarity. In our study, the decision tree’s optimal size was determined through cross-validation. This process entailed pruning the tree to its most effective dimensions, thereby enhancing predictive accuracy. The model was applied to the test set to evaluate its effectiveness.
   
## Results

![table2](https://github.com/sangyisu/625-project/assets/117102360/b869b85d-3aa5-4c97-8a1f-8877cfb0a735)

Post-optimization, the models' accuracy was evaluated using diverse machine learning techniques. As shown in the table above, the logistic regression model achieved an accuracy of 0.8967, while the SVM model reached 0.9133. The Naive Bayes model attained 0.7209, the Random Forest model recorded 0.8961, and the Decision Tree model yielded an accuracy of 0.8764.




