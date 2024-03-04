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
# Data cleaning:
```py
import pandas as pd
import numpy as np
import seaborn as sns
import os 
df=pd.read_csv("SAMPLEIDS.csv")
df
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/6534a3d9-b581-4aef-a6fb-3fa27e6418b6)
```py
df.isnull().sum()
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/75492be5-e008-40d4-8e07-06b3736a89fb)
```py
df.isnull().any()
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/8b053ef6-365a-4ba4-9cf9-3292ce288dc4)
```py
df.dropna()
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/450cc17d-6c5e-4490-88ea-7b5a1fabff23)
```py
df.fillna(0)
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/8fb047b1-0a76-4d05-ba34-3c354f63b580)
```py
df.fillna(method = 'ffill')
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/1f9f3a5a-c7e2-4bf4-aa94-18aaaedda7be)
```py
df.fillna(method = 'bfill')
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/ef27d752-eb66-452f-aa46-62a9829804fb)
```py
df_dropped = df.dropna()
df_dropped
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/3aa259d7-02d7-4584-a60d-5ecfd35c6d89)
```py
df.fillna({'GENDER':'FEMALE','NAME':'PRIYU','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/e2676988-2a63-46f8-9e23-068e0ea644c2)
## IQR(Inter Quartile Range):
```py
import pandas as pd
```
```py
ir=pd.read_csv('iris.csv')
ir
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/f64f8081-b37c-4c2d-ade0-2040460b19e5)
```py
ir.describe()
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/2bb7225e-a976-456b-8530-a0dd15668fd1)
```py
import seaborn as sns
```
```py
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/e2fa7ff8-9d0f-4d28-b1ff-63406532caa6)
```py
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/c5cc693b-e266-474d-b840-f6ff5b2937c2)
```py
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/785c09e7-25e9-4a08-9fcd-92970c6df6c4)
```py
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/b7ddd65d-7384-4f8c-b13b-dc7563c1ddf9)
```py
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/04b38063-f18e-489c-8391-0540950c4d78)
## Z score:
```py                            
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
```
```py
dataset=pd.read_csv("heights.csv")
dataset
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/c0aff136-18fd-4e0d-bc44-54c521438496)
```py
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
```
```py
iqr = q3-q1
iqr
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/29935765-99ce-4650-99df-96da5b69f3e9)
```py
low = q1 - 1.5*iqr
low
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/6e7332ba-bb7a-4a07-bf1d-8c663953ae2f)
```py
high = q3 + 1.5*iqr
high
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/b2a02bc0-69fe-4cd4-9496-ca933582f52f)
```py
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/4684ddc3-f251-4f5e-8b42-54ff73e19b5a)
```py
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/9a451553-20c3-4503-9842-6ef06c92f108)
```py
df1 = df[z<3]
df1
```
![image](https://github.com/Moonesh0805/exno1/assets/138849189/a989a05c-df8a-45a8-9052-70c6d58361fe)

# Result
 Hence the data was cleaned , outliers were detected and removed.
