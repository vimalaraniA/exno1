# Exno:1
Data Cleaning Process

NAME:VIMALA RANI A

REG NO:212223040240

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
##  Data Cleaning
#### READ CSV FILE 
   
import pandas as pd

df=pd.read_csv('Loan_data.csv')

df

![Screenshot 2025-03-13 154512](https://github.com/user-attachments/assets/159aa56c-2171-4e35-9836-bffa5f694964)

#### DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS


df.info()

![Screenshot 2025-03-13 160759](https://github.com/user-attachments/assets/7d794af1-9fde-491d-ad15-0a2b76072b73)

df.describe()

![Screenshot 2025-03-13 154539](https://github.com/user-attachments/assets/c5d90215-84e4-4a7a-87e3-16cb56641bd2)

#### CHECK OUT NULL VALUES IN DATA SET USING FUNCTION

df.isnull()

![Screenshot 2025-03-13 154552](https://github.com/user-attachments/assets/877ebd35-8b1c-4806-90ca-2e14b93e95da)

#### DISPLAY THE SUM ON NULL VALUES IN EACH ROWS

df.isnull().sum()

![Screenshot 2025-03-13 154603](https://github.com/user-attachments/assets/aa5be461-fa66-481d-bf7f-e7bed73a8d33)

#### DROP NULL VALUES

df_dropped=df.dropna()

df_dropped

![Screenshot 2025-03-13 154613](https://github.com/user-attachments/assets/6aa7bd01-938e-4030-9ea7-ace39d99c057)

#### FILL NULL VALUES WITH CONSTANT VALUE "O"
     

df_fill_0=df.fillna(0)

df_fill_0

![Screenshot 2025-03-13 154625](https://github.com/user-attachments/assets/3d784f9e-01f6-42e7-a7bc-4041e363848a)

#### FILL NULL VALUES WITH ffill or bfill METHOD

df_ffill=df.ffill()

df_ffill

![Screenshot 2025-03-13 154637](https://github.com/user-attachments/assets/c3390e62-e72c-4d72-a541-d543693aa3db)




df_bfill=df.bfill()

df_bfill

![Screenshot 2025-03-13 154650](https://github.com/user-attachments/assets/1d26521c-04a5-487f-965b-37fb545b8c9d)

#### CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES

df_new=df

df_new['LoanAmount']=df['LoanAmount'].fillna((df['LoanAmount']).mean)

df_new['Loan_Amount_Term']=df['Loan_Amount_Term'].fillna((df['Loan_Amount_Term']).mean)

df_new


![Screenshot 2025-03-13 154702](https://github.com/user-attachments/assets/cd622433-f438-40df-937e-7d4c55d5b3e9)

#### DROP NULL VALUES
     


df_new.dropna(axis=0)

![Screenshot 2025-03-13 154714](https://github.com/user-attachments/assets/5c0a209d-763f-46a0-b5c0-e1cc219ceac2)

## Outlier Detection and Removal

import pandas as pd

import seaborn as sns

age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]

af=pd.DataFrame(age)

af

![Screenshot 2025-03-13 154728](https://github.com/user-attachments/assets/c14a0c29-c39e-41f1-a2c7-d1de926cadc3)

#### USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER


sns.boxplot(data=af)

![Screenshot 2025-03-13 154739](https://github.com/user-attachments/assets/151ddb61-0f95-4921-8d06-c94f5bb91242)

#### PERFORM IQR METHOD AND DETECT OUTLIER VALUES

import numpy as np

Q1=np.percentile(age,25)

Q2=np.percentile(age,50)

Q3=np.percentile(age,75)



ivr=Q3-Q1

lower_bound=Q1-1.5*IQR

upper_bound=Q3+1.5*IQR

outliers=af[(af<lower_bound) | (af>upper_bound) ]



print("Quantile 1",Q1)

print("Quantile 2",Q2)

print("Quantile 3",Q3)

print("Inter Quartile Range",IQR)

print("Lower Bound",lower_bound)

print("Upper Bound",upper_bound)

print("Outliers",outliers)


![Screenshot 2025-03-13 154753](https://github.com/user-attachments/assets/4808da3e-6e04-43c7-aa08-9e74b58734a2)

#### REMOVE OUTLIERS

af=af[(af>=lower_bound) & (af<=upper_bound)]
af.dropna()
print("After removing outliers")
af

![Screenshot 2025-03-13 154803](https://github.com/user-attachments/assets/07d0ab7a-bd52-4063-b8f9-8eefb26e3e8a)

#### USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED


sns.boxplot(data=af)

![Screenshot 2025-03-13 154815](https://github.com/user-attachments/assets/601c33fb-7f0d-4fc8-a18c-f81892740d9f)

#### USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER

from scipy import stats

data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]

df=pd.DataFrame(data)

sns.boxplot(data=df)


![Screenshot 2025-03-13 154827](https://github.com/user-attachments/assets/095f1b1b-3dc2-49f7-bcff-9a5d176eb832)

#### PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES

z=np.abs(stats.zscore(data))

print("Outlier values:")

outliers=df[z>3]

outliers

![Screenshot 2025-03-13 154839](https://github.com/user-attachments/assets/fd1b31e0-49fe-4a9c-b987-75c75dd1b695)

#### REMOVE OUTLIERS

cleaned_df=df[z<3]

print("After removing outliers")

cleaned_df


![Screenshot 2025-03-13 154853](https://github.com/user-attachments/assets/59dc72df-87cc-4261-a536-3b76d680fd0d)


#### USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED

sns.boxplot(data=cleaned_df)

![Screenshot 2025-03-13 154904](https://github.com/user-attachments/assets/84d3b6f6-30be-4618-81c1-225c944b643a)




# Result
Thus the data cleaning process on the given dataset is executed successfully.
