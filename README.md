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
```
import pandas as pd
import numpy as np
import seaborn as sns
import os 
df=pd.read_csv("SAMPLEIDS.csv")
df
```
<img width="762" height="660" alt="image" src="https://github.com/user-attachments/assets/b13b1c82-1283-4589-a5aa-d1d25a573faa" />

```
df.isnull().sum()
```
<img width="134" height="418" alt="image" src="https://github.com/user-attachments/assets/a9b4a79f-0b56-4d2f-a0c9-656a2f50fbcd" />

```
df.isnull().any()
```
<img width="157" height="430" alt="image" src="https://github.com/user-attachments/assets/cd9797dc-5e6c-4dfd-be1a-2b57335d5965" />

```
df.dropna()
```
<img width="773" height="422" alt="image" src="https://github.com/user-attachments/assets/74984220-e429-4f62-ab86-02c5e6361de3" />

```
df.fillna(0)
```
<img width="758" height="647" alt="image" src="https://github.com/user-attachments/assets/f6b2f2a3-6747-4afb-bb7f-4a37a8e00b31" />

```
df.fillna(method = 'ffill')
```
<img width="771" height="673" alt="image" src="https://github.com/user-attachments/assets/78de9b6d-dfd2-4c49-a007-f79e8235adf7" />

```
df.fillna(method = 'bfill')
```
<img width="768" height="676" alt="image" src="https://github.com/user-attachments/assets/ada32ef7-23ec-4e2c-b253-e85aa2298ddb" />

```
df_dropped = df.dropna()
df_dropped
```
<img width="823" height="458" alt="image" src="https://github.com/user-attachments/assets/91123dc2-3d54-4574-8bed-6ac4a5fc2670" />

```
df.fillna({'GENDER':'FEMALE','NAME':'PRIYU','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
<img width="832" height="716" alt="image" src="https://github.com/user-attachments/assets/41e96e16-467b-4070-be5e-e67d2ca03b25" />

## IQR(Inter Quartile Range):
```
import pandas as pd
ir=pd.read_csv('iris.csv')
ir
```
<img width="507" height="375" alt="image" src="https://github.com/user-attachments/assets/c1af8203-edb2-45b1-90d5-a03d44d0fcb8" />

```
ir.describe()
```
<img width="448" height="275" alt="image" src="https://github.com/user-attachments/assets/0f32fff9-5970-4f4f-aad5-e4a59e8edef4" />

```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
<img width="520" height="431" alt="image" src="https://github.com/user-attachments/assets/76537797-d7c1-4f53-88e5-6ddd81e626e8" />

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```
![image](https://github.com/dharshan7200/exno1/assets/138850116/743ab1d5-b07b-4851-ae77-b134525afc42)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
<img width="500" height="376" alt="image" src="https://github.com/user-attachments/assets/33d7051c-0dfc-447f-bce9-16382073a97f" />

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
<img width="529" height="437" alt="image" src="https://github.com/user-attachments/assets/9bbbcda6-ba8c-4b35-a210-719747dfa227" />

```
sns.boxplot(x='sepal_width',data=delid)
```

<img width="176" height="447" alt="image" src="https://github.com/user-attachments/assets/e2a2fac7-4d89-4273-a736-43adf5815e1f" />

## Z score:
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("heights.csv")
dataset
```
<img width="176" height="447" alt="image" src="https://github.com/user-attachments/assets/1feb11f3-3178-48cf-9399-94298584749a" />

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
<img width="230" height="29" alt="image" src="https://github.com/user-attachments/assets/48c8c141-b5c9-4b28-9777-d11a4b717b3a" />

```
low = q1 - 1.5*iqr
low
```
<img width="225" height="33" alt="image" src="https://github.com/user-attachments/assets/a8c13841-479b-47b8-bc2f-c101f44f5cba" />

```
high = q3 + 1.5*iqr
high
```
<img width="142" height="36" alt="image" src="https://github.com/user-attachments/assets/b0e3083e-55a0-4484-835a-a1fe13e6adda" />

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
<img width="156" height="398" alt="image" src="https://github.com/user-attachments/assets/41f9a224-3b5d-4561-b732-e076fd41858a" />

```
z = np.abs(stats.zscore(df['height']))
z
```
<img width="505" height="73" alt="image" src="https://github.com/user-attachments/assets/dc07c7be-5298-40f3-b77b-1ea2d1742fa1" />

```
df1 = df[z<3]
df1
```
<img width="166" height="427" alt="image" src="https://github.com/user-attachments/assets/34316df5-1650-4f6a-ab18-12e30cf2a42c" />


## Result:

Hence the data was cleaned , outliers were detected and removed.
