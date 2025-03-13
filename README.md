# Exno:1
Data Cleaning Process

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

![image](https://github.com/user-attachments/assets/cb677b6c-086a-46ec-87d9-2a3a736d1cca)
#### DISPLAY THE INFORMATION ABOUT CSV AND RUN THE BASIC DATA ANALYSIS FUNCTIONS


df.info()

![image](https://github.com/user-attachments/assets/6342c7a3-96b1-49f9-9dc1-3d642acfa0c7)


df.describe()

![Screenshot 2025-03-12 205741](https://github.com/user-attachments/assets/2e5196ce-2086-43c2-88ea-c850ca86f18f)
#### CHECK OUT NULL VALUES IN DATA SET USING FUNCTION

df.isnull()

![Screenshot 2025-03-12 205944](https://github.com/user-attachments/assets/40256420-d6b8-4682-a1b7-a4d853048bd5)
#### DISPLAY THE SUM ON NULL VALUES IN EACH ROWS

df.isnull().sum()

![Screenshot 2025-03-12 210142](https://github.com/user-attachments/assets/8d18b6ae-a27e-4860-b9f1-9cc19826da56)
#### DROP NULL VALUES

df_dropped=df.dropna()
df_dropped

![Screenshot 2025-03-12 210251](https://github.com/user-attachments/assets/830b54d2-51a2-4ecf-ae9b-34202e51121d)
#### FILL NULL VALUES WITH CONSTANT VALUE "O"
     

df_fill_0=df.fillna(0)
df_fill_0

![Screenshot 2025-03-12 210541](https://github.com/user-attachments/assets/8159e4c6-d3be-4ea8-bd0a-5aae132bf868)
#### FILL NULL VALUES WITH ffill or bfill METHOD

df_ffill=df.ffill()
df_ffill

![Screenshot 2025-03-12 210650](https://github.com/user-attachments/assets/a5136bd3-67d9-4cbc-a2a8-572a5949f949)



df_bfill=df.bfill()
df_bfill

![Screenshot 2025-03-12 210748](https://github.com/user-attachments/assets/5b0a9387-2f22-4755-aa0c-bd46cc2d3037)
#### CALCULATE MEAN VALUE OF A COLUMN AND FILL IT WITH NULL VALUES

df_new=df
df_new['LoanAmount']=df['LoanAmount'].fillna((df['LoanAmount']).mean)
df_new['Loan_Amount_Term']=df['Loan_Amount_Term'].fillna((df['Loan_Amount_Term']).mean)
df_new

![Screenshot 2025-03-12 211027](https://github.com/user-attachments/assets/fc4297da-3843-431c-b0db-aac6afae1c30)
#### DROP NULL VALUES
     


df_new.dropna(axis=0)

![Screenshot 2025-03-12 211147](https://github.com/user-attachments/assets/b5c0f382-9e83-4fda-995d-439169d6f452)

## Outlier Detection and Removal

import pandas as pd
import seaborn as sns
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af

![Screenshot 2025-03-12 211733](https://github.com/user-attachments/assets/c1ec6ba9-ed36-49cc-b328-6f8e309581af)
#### USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER


sns.boxplot(data=af)

![Screenshot 2025-03-12 211817](https://github.com/user-attachments/assets/005d6813-9cda-4a92-9e5f-4cd29f721192)
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

![Screenshot 2025-03-12 212108](https://github.com/user-attachments/assets/96295492-fe39-40a7-9931-56a6c9739c65)
#### REMOVE OUTLIERS

af=af[(af>=lower_bound) & (af<=upper_bound)]
af.dropna()
print("After removing outliers")
af

![Screenshot 2025-03-12 212250](https://github.com/user-attachments/assets/188b7ac3-7e1b-4a37-8a5e-a5274409dc6b)
#### USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED


sns.boxplot(data=af)

![image](https://github.com/user-attachments/assets/b9c8bc6d-2102-4ca6-b5d4-53c65738b586)

#### USE BOXPLOT FUNCTION HERE TO DETECT OUTLIER

from scipy import stats
data=[1,12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,72,75,78,81,84,87,90,93,96,99,158]
df=pd.DataFrame(data)
sns.boxplot(data=df)

![image](https://github.com/user-attachments/assets/9d7f81ad-2ad1-41bc-bb47-059683b81f4e)

#### PERFORM Z SCORE METHOD AND DETECT OUTLIER VALUES

z=np.abs(stats.zscore(data))
print("Outlier values:")
outliers=df[z>3]
outliers

![image](https://github.com/user-attachments/assets/a4274bdd-9fe7-4c6b-8f3c-645276230b1d)

#### REMOVE OUTLIERS

cleaned_df=df[z<3]
print("After removing outliers")
cleaned_df

![Screenshot 2025-03-12 220938](https://github.com/user-attachments/assets/51987019-80da-4500-a190-3f29f00edcd5)

#### USE BOXPLOT FUNCTION HERE TO CHECK OUTLIER IS REMOVED

sns.boxplot(data=cleaned_df)

![Screenshot 2025-03-12 221025](https://github.com/user-attachments/assets/dbadfda8-fac1-4505-bfef-a39220b3cbd0)



# Result
Thus the data cleaning process on the given dataset is executed successfully.
