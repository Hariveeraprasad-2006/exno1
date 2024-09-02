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

# Coding and Output:
# STEP 1: Read the given Data
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
```
# STEP 2: Get the information about the data
```
df.info()
```
# OUTPUT:
![image](https://github.com/user-attachments/assets/f329c9ab-d5b8-4da8-9a92-de59dbe37c52)
# STEP 3: Remove the null values from the data
```
df['NAME'].fillna(df['NAME'].mode()[0], inplace=True)
df['GENDER'].fillna(df['GENDER'].mode()[0], inplace=True)
df['ADDRESS'].fillna(df['ADDRESS'].mode()[0], inplace=True)
df['M1'].fillna(df['M1'].mean(), inplace=True)
df['M2'].fillna(df['M2'].mean(), inplace=True)
df['M3'].fillna(df['M3'].mean(), inplace=True)
df['M4'].fillna(df['M4'].mean(), inplace=True)
df['TOTAL'].fillna(df[['M1', 'M2', 'M3', 'M4']].sum(axis=1), inplace=True)
df['AVG'].fillna(df['TOTAL'] / 4, inplace=True)
df['DOB_MISSING'] = df['DOB'].isna()
```
## OUTPUT:
# NULL VALUES IN THE DATA:
![image](https://github.com/user-attachments/assets/68a5ee8f-3c7a-41fb-a6a0-f6e45a9f4476)
# AFTER HANDLING USING MEAN AND MODE:
![image](https://github.com/user-attachments/assets/81232b89-05d3-49a3-b34f-ccf84c80786f)
# STEP 4: Remove outliers using IQR:
```
Q1 = df[['M1', 'M2', 'M3', 'M4', 'TOTAL', 'AVG']].quantile(0.25)
Q3 = df[['M1', 'M2', 'M3', 'M4', 'TOTAL', 'AVG']].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[['M1', 'M2', 'M3', 'M4', 'TOTAL', 'AVG']] < (Q1 - 1.5 * IQR)) |(df[['M1', 'M2', 'M3', 'M4', 'TOTAL', 'AVG']] > (Q3 + 1.5 * IQR))).any(axis=1)]
```
# STEP 5: Use zscore of to remove outliers
```
from scipy import stats
z_scores = stats.zscore(df.select_dtypes(include=['float64', 'int64']))
df_no_outliers_zscore = df[(abs(z_scores) < 3).all(axis=1)]
```
# DATA AFTER CLEANING:
![image](https://github.com/user-attachments/assets/f6df62b1-bbfc-4a54-9c5b-4f85e315b130)

# Result:
BY USING THIS CODE WE CAN HANDLE THE MISSING VALUES AND CAN REMOVE THE OUTLIERS.
