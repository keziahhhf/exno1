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
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/b5b44c4b-4108-46a0-bc78-65a1d0a2d6da)

```
df.shape
```
![image](https://github.com/user-attachments/assets/593e367f-0789-4160-bcc9-1056afd90262)

```
df.describe()
```
![image](https://github.com/user-attachments/assets/ccb4e728-a07d-4a4a-a86c-57afbe89b834)

```
df.info()
```
![image](https://github.com/user-attachments/assets/f400d3f2-d94f-489b-9f68-79dd7f74d046)

```
df.head(3)
df.tail(3)
```
![image](https://github.com/user-attachments/assets/c7dcb1ed-2977-48d7-8a4a-82a116202f52)
```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/3c4564f5-273a-4df8-8093-50052c32e054)
```
df.dropna(how='any').shape
```
![image](https://github.com/user-attachments/assets/ae7c08ad-7fea-48e9-be18-12dfb71b1c5d)
```
mn=df.TOTAL.mean()
```
![image](https://github.com/user-attachments/assets/dd560c24-2836-4581-bd30-6bd26800883e)
```
mn
```
![image](https://github.com/user-attachments/assets/8adb0353-1b5c-429b-8cef-bca6e5585841)

```
df.TOTAL.fillna(mn,inplace=True)
df
```
![image](https://github.com/user-attachments/assets/e7ee36e9-2e34-4b22-9881-240d65ac864d)
```
df.M1.fillna(method='FFill',inplace=True)
df
```
df.isna().sum()
```

![image](https://github.com/user-attachments/assets/05f02b16-ed52-4742-b1fa-4d37ccd739bb)
```
df.M2.dropna(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/5e8d0d18-facb-42a4-a041-8078e9d09d6c)
```
df.drop_duplicates(inplace=True)
df
```
![image](https://github.com/user-attachments/assets/74dcc5e7-5186-4120-b316-5830baf34c02)
```
df.duplicated()
```
![image](https://github.com/user-attachments/assets/9ed61054-93ce-4ee6-bfb2-d2b3c2d53bcc)
```
df['DOB']
```
![image](https://github.com/user-attachments/assets/afcf88ba-0285-4052-83f3-363e963ff855)
```
df['DOB']=pd.to_datetime(df['DOB'],format='%Y-%m-%d',errors='coerce')
df
```
![image](https://github.com/user-attachments/assets/db84a748-d353-4ea1-a83a-97219e51a9b7)
```
import seaborn as sns
sns.heatmap(df.isnull(), yticklabels=False,annot=True)
```
![image](https://github.com/user-attachments/assets/18ff5c41-8ad2-4152-b4b2-9c5a952d3765)

# OUTLIER DETECTION AND REMOVAL USING IQR

```
import pandas as pd
import seaborn as sns
import numpy as py
age={1,3,28,27,25,92,30,39,40,50,26,24,29,94}
af=pd.DataFrame(age)
af
```
![image](https://github.com/user-attachments/assets/9ad1e4ae-ef6a-4d9e-8d68-b35110908113)


```
sns.scatterplot(data=af)

```

![image](https://github.com/user-attachments/assets/53385e2c-36e9-42ad-a4ff-b55d7af8443b)

```
sns.boxplot(data=af)
```

![image](https://github.com/user-attachments/assets/fcbfc0a1-461c-46e4-984c-27c245e0fdee)

```
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```

![image](https://github.com/user-attachments/assets/8861e2b4-93ce-49aa-b23d-9e62e9375b46)

```
lower_bound=Q1-(1.5*IQR)
upper_bound=Q3+(1.5*IQR)
lower_bound,upper_bound
```

![image](https://github.com/user-attachments/assets/ca3b1887-0d13-4b1b-9456-80a5821b273e)


```
outliers = [x for x in age if (x < lowerbound.iloc[0]) or (x > upper_bound.iloc[0])]
# Extract the numeric values from the Series for comparison
print("q1",q1)
print("q3",q3)
print("iqr",iqr)
print("lower bound",lowerbound)
print("upper bound",upper_bound)
print("outliers",outliers)
```

![image](https://github.com/user-attachments/assets/7198c3bc-e6e1-44f3-ba0c-adde0143ad56)

```
import numpy as np

data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print("mean:",mean)
print("std",std)
```
![image](https://github.com/user-attachments/assets/e382e367-b892-4d9f-9b16-13914cedb6ca)


```
threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z>threshold:
    outlier.append(i)
    print('Outlier in dataset is:',outlier)
```

![image](https://github.com/user-attachments/assets/ae5c802a-aa5c-4c78-85a6-8df8f7caaf2d)


```
import scipy as stats
data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}
df=pd.DataFrame(data)
df

```

![image](https://github.com/user-attachments/assets/46328336-91e7-42d1-b561-73b78e6a3736)


```
df=pd.DataFrame(data)
df

z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
```

![image](https://github.com/user-attachments/assets/bb0eb7f2-1e5e-49fb-b146-56cb36c219ba)
```
val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]

import numpy as np
out=[]
def d_o(val):
  ts=3
  m=np.mean(val)
  sd=np.std(val)
  for i in val:
    z=(i-m)/sd
    if np.abs(z)>ts:
      out.append(i)
  return out

op=d_o(val)

op
```

![image](https://github.com/user-attachments/assets/45c3f29e-cf72-4b0b-a520-ccc793f16e4f)

# Result
    Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
