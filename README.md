# Prevalence-of-Diabetes-Amongst-Pima-Indian-Women
A population of women who were at least 21 years old, of Pima Indian heritage and living near Phoenix, Arizona, was tested for diabetes according to World Health Organization criteria. The data were collected by the US National Institute of Diabetes and Digestive and Kidney Diseases.

Prevalence-of-Diabetes-Amongst-Pima-Indian-Women
A population of women who were at least 21 years old, of Pima Indian heritage and living near Phoenix, Arizona, was tested for diabetes according to World Health Organization criteria. The data were collected by the US National Institute of Diabetes and Digestive and Kidney Diseases.

import numpy as np
import pandas as pd

import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline 

#NumPy: Allows us to perform mathematical functions on arrays as well as adding data structure.
#Pandas: Processes data, allowing us to create data structures and manipulate data and allows us to generate analytical conclusions.
#Seaborn: A visualisation library which better helps us understand and evaluate our data to bring us informative explanatory data analysis. 
#Matplotlib: The Matplotlib library is used for visualisation purposes and allows us certain plotting techniques, export to a variety of file formats and customise over different visual styles

pd.read_csv('/Users/marcusdoty/Downloads/diabetes.csv')

pima = pd.read_csv('/Users/marcusdoty/Downloads/diabetes.csv')

pima.tail(10)

pima.head(10)

pima.shape

pima.info()

pima.isnull().values.any()

pima.iloc[:,0:8].describe()

sns.displot(pima['BloodPressure'], kind='kde')
plt.show()
#The distribution for the blood pressure is very symmetrical with almost all of the observations lying between 40 and 100. Most observations are around 70 with the a very high peak, representing most observations in the middle and little standard deviation per observation. Furthermore there appears to be a heavier right tail indicating a higher concentration of the sample lives there – higher blood pressure.

pima.sort_values('Glucose')
#The highest level of Glucose in this study is 199, their corresponding BMI is 42.9.

m1 = pima['BMI'].mean()
print(m1)
m2 = pima['BMI'].median()
print(m2)
m3 = pima['BMI'].mode()[0]
print(m3)

pima[pima['Glucose']>pima['Glucose'].mean()].shape[0]

sns.pairplot(data=pima,vars=['Glucose','SkinThickness','DiabetesPedigreeFunction'], hue='Outcome')
plt.show()

#As we can see there are notable disparities in the distribution of the data given if you do or do not have diabetes. The distribution chart in the top left tells us that those who have diabetes have recorded higher levels of glucose with a higher mean, mode and median – they also have a more varied distribution. This is the most obvious observation. It also seems prevalent that those with diabetes have thicker skin with a higher concentration of the sample population as far as mean and median in the scatterplot in the middle row, first column. Those who did not record diabetes also tend to have less dispersion amongst the sample population and tend to be a lot closer together. The diabetes pedigree function distribution chart in the bottom right also tells us that much of the non-diabetic sample are in the middle of their function and is a very high peak, whereas the diabetic sample tends to have a much heavier right tail. 

sns.scatterplot(x='Glucose',y='Insulin',data=pima)
plt.show()

#The data that shows the correlation between insulin and glucose gives us a pretty strong indicator that these two are strongly related and we may even be able to draw a credible line of best fit. Much of the sample tends to have a glucose concentrated around 80-140 U/ml, although there is a considerable amount of outliers that have a higher glucose and insulin concentration ranging up to 200 U/ml. At the same time, the level of insulin doesn’t tend to be as varied, with around three quarters sitting under 200 – with some very high relative outliers – one at over 800.

plt.boxplot(pima['Age'])

plt.title('Boxplot of Age')
plt.ylabel('Age')
plt.show()

#Some outliers do exist with some of the sample the age of some of the sample being over 70 and some one lady being 80.

plt.hist(pima[pima['Outcome']==1]['Age'], bins = 5)
plt.title('Distribution of Age for Women who has Diabetes')
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.show()

plt.hist(pima[pima['Outcome']==0]['Age'], bins = 5)
plt.title('Distribution of Age for Women who do not have Diabetes')
plt.xlabel('Age')
plt.ylabel('Frequency')
plt.show()
#As we can see, diabetes does affect women of all ages, given that most women sampled were in their 20s and 30s, there is a much higher frequency of diabetes in these younger women. The frequency distribution then tends to drop as you get older which makes sense given that not as many older women were sampled. On the other side, around 350 women who were in their 20s did not have diabetes (vs 90 women who did have diabetes – a ratio of 4 to 1) and this drops of dramatically to women in their 30s and this balance tends to become more even (around 80 women did have diabetes in their 30s vs 100 who did not). This trend becomes a little prevalent with women in their 40s with a ratio of 60 with diabetes to 90 without diabetes. Women in their 50s are much more balanced, however women in their 60s have a much more disproportionate ratio – more women who did not record diabetes. 

Q1 = pima.quantile(0.25)
Q3 = pima.quantile(0.75)
IQR = Q3 - Q1
print(IQR)

corr_matrix = pima.iloc[:,0:8].corr()

corr_matrix

#1 Pregnancy and age have strongest correlation amongst all variables indicating that older women are having relatively more pregnancies. 
#2 Skin thickness and BMI also hold a relatively high correlation (0.53) which tells us that those who have a higher BMI are more likely to be prevalent with a higher tricep skinfold thickness.
#3 Both insulin and glucose have a strong relative correlation (0.4) which tells us that the sample who scored higher in their plasma glucose concentration test also tend to record a higher response rate for their insulin reading and vice versa.
#4 Blood pressure and age have a strong correlation (0.33) which tells us that as you become older you are more inclined to face problems relating to a higher blood pressure.
#5 BMI and blood pressure also share a higher relatively correlation (0.28) which indicates that someone with a higher blood pressure is also likely to have a higher BMI score. 

plt.figure(figsize=(8,8))
sns.heatmap(corr_matrix, annot = True)
plt.show()
