#EX.NO:1
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

# Coding and Outut
```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
df= pd.read_csv("D:\Dataset.csv")
df = df.dropna(subset=["show_name"])
df["aired_on"] = df["aired_on"].ffill()
df = df.dropna(subset=["current_overall_rank"])
df = df.dropna(subset=["original_network"])
df["rating"] = df["rating"].fillna(df["rating"].mean())
df["watchers"] = df["watchers"].fillna(df["watchers"].mean())

df


print(df.isnull().sum())

sns.boxplot(x=df["watchers"])
plt.show()

Q1 = df["watchers"].quantile(0.25)
Q3 = df["watchers"].quantile(0.75)
IQR=Q3-Q1
LF = Q1 - 1.5 * IQR
UF = Q3 + 1.5 * IQR
print("lower_fence\n",LF)
print("upper_fence\n",UF)
print("Outliers detected:")
print(df[(df["watchers"] < LF) | (df["watchers"] > UF)])
df = df[(df["watchers"] >= LF) & (df["watchers"] <= UF)]
print("Outliers removed")
```
<img width="1458" height="789" alt="Screenshot 2025-12-01 100817" src="https://github.com/user-attachments/assets/3998ab3b-cd11-41dd-b1c2-c2e38a0b2397" />
<img width="1430" height="679" alt="Screenshot 2025-12-01 100957" src="https://github.com/user-attachments/assets/0d1c99ad-ba42-4e78-9465-5220eb17ac7d" />
<img width="1421" height="625" alt="Screenshot 2025-12-01 101340" src="https://github.com/user-attachments/assets/6cc6535b-f20e-4620-ba10-224d227b1828" />
<img width="1363" height="661" alt="Screenshot 2025-12-01 101702" src="https://github.com/user-attachments/assets/856063fc-320f-41e7-be3a-a52a8e4ad853" />




# Result
thus,the data cleaning process has been completed successfully.
