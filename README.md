# Ex02-Outlier

You are given bhp.csv which contains property prices in the city of banglore, India. You need to examine price_per_sqft column and do following,

(1) Remove outliers using IQR 

(2) After removing outliers in step 1, you get a new dataframe.

(3) use zscore of 3 to remove outliers. This is quite similar to IQR and you will get exact same result

(4) for the data set height_weight.csv find the following

    (i) Using IQR detect weight outliers and print them

    (ii) Using IQR, detect height outliers and print them
## AIM:
TO detect and remove the outliers in the given data set and save the final data.

## Algorithm:
## Step 1
Import the required packages(pandas,numpy,scipy)

## Step 2
Read the given csv file

## Step 3
Convert the file into a dataframe and get information of the data.

## Step 4
Remove the non numerical data columns using drop() method.

## Step 5
Detect the outliers in the data set using z scores method.

## Step 6
Remove the outliers by z scores and list manupilation or by using Interquartile Range(IQR)

## Step 7
Check if the outliersare removed from data set using graphical methods.

## Step 8
Save the final data set into the file.

## Program:
### (1) Examine price_per_sqft column and use IQR to remove outliers and create new dataframe
```
import pandas as pd
import seaborn as sns
df = pd.read_csv("/content/bhp.csv")
df
sns.boxplot(data=df)
sns.boxplot(x="price_per_sqft",data=df)
q1 = df['price_per_sqft'].quantile(0.35)
q3 = df['price_per_sqft'].quantile(0.65)
print("First Quantile =",q1,"\nSecond Quantile =",q3)
IQR = q3-q1
high = q3+1.5*IQR
low = q1-1.5*IQR
df1 =df[((df['price_per_sqft']>=low)&(df['price_per_sqft']<=high))]
df1
sns.boxplot(x="price_per_sqft",data=df1)
df1.shape
```
## (1) & (2) Examine price_per_sqft column and use zscore of 3 to remove outliers.
```
from scipy import stats
import numpy as np
z = np.abs(stats.zscore(df['price_per_sqft']))
df2 = df[(z<3)]
df2
df2.shape
sns.boxplot(x="price_per_sqft",data=df2)
```
## (4) (i)For the data set height_weight.csv detect weight outliers using IQR method
```
df3 = pd.read_csv("/content/height_weight.csv")
df3
sns.boxplot(x="weight",data=df3)
q1 = df3["weight"].quantile(0.25)
q3 = df3['weight'].quantile(0.75)
print("First Quantile = ",q1,"\nSecond Quantile = ",q3)
IQR = q3-q1
low = q1-1.5*IQR
high = q3+1.5*IQR
df4 =df3[((df3['weight']>=low)&(df3['weight']<=high))]
df4
df4.shape
sns.boxplot(x="weight",data=df4)
```
## (4)(ii) For the data set height_weight.csv detect height outliers using IQR method.
```
sns.boxplot(x="height",data=df3)
q1 = df3["height"].quantile(0.25)
q3 = df3['height'].quantile(0.75)
print("First Quantile = ",q1,"\nSecond Quantile = ",q3)
IQR = q3-q1
low = q1-1.5*IQR
high = q3+1.5*IQR
df5 =df3[((df3['height']>=low)&(df3['height']<=high))]
df5
df5.shape
sns.boxplot(x="height",data=df5)
```
## OUTPUT:
## DATASET FOR bhp.csv
![Screenshot 2023-03-25 223811](https://user-images.githubusercontent.com/113497491/227731875-f834f3a2-99e1-4911-8500-2f44a2086d98.png)
## bhp Boxplot
![Screenshot 2023-03-25 223827](https://user-images.githubusercontent.com/113497491/227731935-edf845ec-75b5-4ebe-91f4-8b8559204363.png)
## DATASET BOXPLOT WITH OUTLIERS(BHP)
![Screenshot 2023-03-25 223838](https://user-images.githubusercontent.com/113497491/227731953-5a76154a-9f77-408e-b08e-9e51a5dee26f.png)
## DATASET WITHOUT OUTLIERS(BHP)
![Screenshot 2023-03-25 223850](https://user-images.githubusercontent.com/113497491/227731965-daa2801d-7b98-468d-87b1-cc7dfcbdd44a.png)
## DATASET BOXPLOT WITHOUT OUTLIERS(BHP)
![Screenshot 2023-03-25 223858](https://user-images.githubusercontent.com/113497491/227731991-ea98bb6d-eef1-4f42-8238-aa57c6a34f11.png)
## Shape
![Screenshot 2023-03-25 223906](https://user-images.githubusercontent.com/113497491/227732009-df6fcbd9-18fd-4ca8-915b-603cb31364e3.png)
## DATASET AFTER REMOVAL OF OUTLIERS USING Z-SCORE(BHP)
![Screenshot 2023-03-25 223916](https://user-images.githubusercontent.com/113497491/227732033-9ebec549-67af-47a6-b177-79ad8f9d9683.png)
## Shape
![Screenshot 2023-03-25 223942](https://user-images.githubusercontent.com/113497491/227732048-8aede8b0-3f1b-45b8-95a4-4e0caf875d27.png)
## DATASET BOXPLOT AFTER REMOVAL OF OUTLIERS USING Z-SCORE(BHP)
![Screenshot 2023-03-25 223959](https://user-images.githubusercontent.com/113497491/227732066-1b3c2123-6082-44f5-8489-51b4c01c7de5.png)
## DATASET FOR WEIGHT_HEIGHT_CSV
![Screenshot 2023-03-25 224010](https://user-images.githubusercontent.com/113497491/227732085-1cd75820-8526-49e5-903f-9683e28f0f62.png)
## DATASET BOXPLOT WITH OUTLIERS(WEIGHT_HEIGHT)
![Screenshot 2023-03-25 224020](https://user-images.githubusercontent.com/113497491/227732111-d6b6be49-0043-45d3-a3c4-487eaa8e3c50.png)
## DATASET AFTER REMOVING OUTLIERS USING IQR METHOD(WEIGHT_HEIGHT)
![Screenshot 2023-03-25 224032](https://user-images.githubusercontent.com/113497491/227732134-10a49964-a520-4e58-a805-35b0e74f7aec.png)
## SHAPE
![Screenshot 2023-03-25 224041](https://user-images.githubusercontent.com/113497491/227732151-f8727bfa-008c-40b2-9c69-c9ebc4099dd7.png)
## DATASET BOXPLOT AFTER REMOVING OUTLIERS USING IQR METHOD(WEIGHT_HEIGHT)
![Screenshot 2023-03-25 224316](https://user-images.githubusercontent.com/113497491/227732177-36b99c50-a556-4602-a2ad-42881de672c4.png)
## FOR HEIGHT COLUMN WITH OUTLIERS
![Screenshot 2023-03-25 225350](https://user-images.githubusercontent.com/113497491/227732373-551ac354-a782-4b40-a68a-c0750d1a5bca.png)
![Screenshot 2023-03-25 225413](https://user-images.githubusercontent.com/113497491/227732390-1d8d48d0-e0fa-4ff6-a3ae-3ed86a641fb0.png)
## Shape
![Screenshot 2023-03-25 225754](https://user-images.githubusercontent.com/113497491/227732449-cd41f9e3-20c6-45ab-8112-35c9e4ff6354.png)
## AFTER REMOVING OUTLIERS BOXPLOT FOR HEIGHT

![Screenshot 2023-03-25 225804](https://user-images.githubusercontent.com/113497491/227732474-9dc66d46-56d2-4d17-81be-42398281af25.png)



