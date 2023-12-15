# Project 625: Prediction of the risk of a Myocardial Infarction or Heart Attack using different Machine Learning 


## preprocessing
- dataset selection
We select the columns with "C15" in names. Thus we get the dataset with information of 2012 survey. And the dataset includes 296320 observations of 88 variables.

- Missing data
1. we select variables with low rate of missing data(<20%), and then we get a dataset with 296320 observations of 81 variables.

2. Due to our binary outcome which is a Myocardial Infarction or Heart Attack(C15CCMI), we delete observations with missing value in this column.

3. we choose the eligiable repondents based on "SAMPLED" and "SFLAG" columns, then we delete three columns named "COHORT","SAMPLED","R15SRVDISP","R15SRVMODE","P15PLREGCDE" and "SFLAG".(we only use baseline information and delete the "COHORT" column where the values are totally same) Thus, we get the dataset named "ori_data.csv" with 296320 obseravtions of 77 variables.

4. do imputation using mice function with 5 iterations. Then, we get the "mice_data29w.csv" file.

## Feature Selection
After deleting the ID column, we have 75+1 features for now in 'completed_data.csv'. First we define most of them are categorical variables and we convert them to factor. Thus, it is more likely to be overfitting when we do Machine Learning Models.

- the structure of the dataset

![Screenshot 2023-12-01 000938](https://github.com/sangyisu/625-project/assets/117102360/b701bc7d-9e98-4ebf-b8f9-9d4b02ca8fba)


- The types of Variables(76)

1.Boolean Variables: "BMICAT"(if obese) "MRSTAT"(if married) "C15READ""C15HEAR""C15CCHBP""C15CC_CAD""C15CC_CHF""C15CCMI""C15CCHRTOTH" "C15CCSTROKE" "C15CC_COPD"  "C15CCGI"     "C15CCARTHIP" "C15CCARTHND" "C15CCOSTEO"  "C15CCSCIATI" "C15CCDIABET" "C15CCANYCA"  "C15DEP2WK"  "C15DEPYR"    "C15DEP2YR"   "C15MUILKG"   "C15PAOADV"   "C15FRMFALL" "C15FRMBAL"   "C15OTOTEST"(26)

2.Oridinal Variables: "AGE"  "EDUC" (2)

3.Nominal Variables: "GENDER" "RACE" "C15VRGENHTH" "C15VRMACT"   "C15VRSTAIR"  "C15VRPACCL"  "C15VRPWORK"  "C15VRMACCL"  "C15VRMWORK"  "C15VRPAIN"  "C15VRCALM"   "C15VRENERGY" "C15VRDOWN"   "C15VRSACT"  "C15VRPHCMP"  "C15VRMHCMP"  "C15ADLBTH"   "C15ADLDRS"   "C15ADLEAT"  "C15ADLCHR"   "C15ADLWLK"   "C15ADLTLT"     "C15CHSTEX"   "C15CHSTRST"  "C15SOBFLT"   "C15SOBSIT"   "C15SOBWLK"   "C15SOBSTR"   "C15FTNUMB"   "C15FTSENS"   "C15FTHC"  "C15FTSRS"    "C15PNART"    "C15PNBACK"   "C15DEPWEEK"  "C15CMPHTH"  "C15SMOKE"    "C15PAOTLK"   "C15FRMTLK"   "C15FRMPREV"  "C15CMPWHO"  "C15SRVDISP"  "C15SRVMODE"    "C15SRVLANG" (47)

4. (number)continuous: "C15HDACT" "C15HDPHY" "C15HDMEN"  "C15PCTCMP" (5)

![Screenshot 2023-11-30 121957](https://github.com/sangyisu/625-project/assets/117102360/6ca97866-a7d7-478a-9369-cf5e2ed15306)

  
- Methods for feature selection
1. Chi-Suquared Feature Selection
   use pair-wise chi-squared test
   
![Screenshot 2023-11-30 201308](https://github.com/sangyisu/625-project/assets/117102360/06996956-b0c6-4ccf-9017-0b65a60324df)


   
3. Mutual Information Feature Selection

## Model Built

- Model Built Using Chi-Squared Features

- Model Built Using Mutual Information Features
