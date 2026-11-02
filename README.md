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

# Coding :
```
import pandas as pd
import numpy as np
from scipy import stats
import matplotlib.pyplot as plt
from sklearn.datasets import load_iris

iris = load_iris()

df = pd.DataFrame(iris.data, columns=iris.feature_names)

df.info()
print(df.describe())

df_null = df.isnull()
print(df_null)

df_null_sum = df.isnull().sum()
print(df_null_sum)

df_nafill_0 = df.fillna(0)
print(df_nafill_0)

df_ffill = df.ffill()
print(df_ffill)

df_bfill = df.bfill()
print(df_bfill)

df_mean1 = df['sepal width (cm)'].fillna(df['sepal width (cm)'].mean())
print(df_mean1)

df_dropna = df.dropna()
print(df_dropna)

clean_data = df.dropna()
clean_data.to_csv('clean_data.csv', index=False)

ir = df.copy()

print(ir)

ir.boxplot()
plt.show()

ir.plot(kind='scatter', x='sepal length (cm)', y='sepal width (cm)')
plt.show()

q1 = ir['sepal width (cm)'].quantile(0.25)
q3 = ir['sepal width (cm)'].quantile(0.75)

iqr = q3 - q1
print(iqr)

rid = ir[
    (ir['sepal width (cm)'] < (q1 - 1.5 * iqr)) |
    (ir['sepal width (cm)'] > (q3 + 1.5 * iqr))
]

print(rid['sepal width (cm)'])

delid = ir[
    ~(
        (ir['sepal width (cm)'] < (q1 - 1.5 * iqr)) |
        (ir['sepal width (cm)'] > (q3 + 1.5 * iqr))
    )
]

print(delid)

data = [
    1, 12, 15, 18, 21, 24, 27, 30, 33, 36,
    39, 42, 45, 48, 51, 54, 57, 60, 63, 66,
    69, 72, 75, 78, 81, 84, 87, 90, 93
]

df = pd.DataFrame(data, columns=['Values'])

mean = np.mean(data)
std = np.std(data)

z = np.abs(stats.zscore(df['Values']))

threshold = 3

outliers = df[z > threshold]

print("Outliers:")
print(outliers)

df_cleaned = df[z <= threshold]

print(df_cleaned)
```


 <h1>Output:</h1>
<img width="707" height="852" alt="Screenshot 2026-11-02 153613" src="https://github.com/user-attachments/assets/c127c9da-cc82-4025-8f7f-afcf1e8376ba" />
<img width="693" height="818" alt="Screenshot 2026-11-02 153626" src="https://github.com/user-attachments/assets/802e261f-9eac-4cf0-8e5e-953f9d5e3f81" />
<img width="637" height="846" alt="Screenshot 2026-11-02 153634" src="https://github.com/user-attachments/assets/570b041d-7a15-47d3-b1e4-1d92e3526bc4" />
<img width="420" height="577" alt="Screenshot 2026-11-02 153654" src="https://github.com/user-attachments/assets/e4f83e39-cb93-497d-83a0-765f3a166edc" />
<img width="430" height="522" alt="Screenshot 2026-11-02 153701" src="https://github.com/user-attachments/assets/d2ab133a-e332-43f2-ab57-e796c8c25dae" />





 
            
<h2>Result:</h2> 
Thus perform data cleaning and save the cleaned data to a file is successfully executed.
