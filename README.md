# Medical Data Analysis

## Abstract

Dataset of personal medical data of 1,338 patients with a variety of variables that have an affect on the cost of medical services provided. The purpose of the analysis is to analyze the effects of variables on the cost of medical care, e.g. age, gender, region, etc. 


## ERD 

![Medical Data ERD](https://user-images.githubusercontent.com/112409778/228036499-add02f0a-54b8-4a90-90f9-47e71c843ef0.png)

## Variables

There are a variety of variables that will impact the outcome of this analysis:

- Age: age of primary beneficiary
  - Teen:13-19 
  - Adult: 20-39 
  - Middle Age Adult : 40-59 	
  - Senior Adult :60+
- Sex: insurance contractor gender,
  - Male 
  - Female
- Body Mass Index (BMI): Weight to height body mass ratio
  - Underweight: Below 18.5
  - Normal: 18.5 - 24.9
  - Overweight: 25.0 – 29.9
  - Obese: Greater Than or equal to 30.0 
- Children: Number of dependents
- Smoker: Smoking
- Region: Region of domicile of the patient in the United States.
  - Northeast 
  - Southeast 
  - Southwest 
  - Northwest
- Charges: Individual medical costs billed by health insurance for services provided

## Objective

The objective of the analysis is to analyze the effects of variables on the cost of medical care. The analysis seeks to answer the following questions:

1. Which region has the lowest cost of medical care?
2. Which gender has the highest typical medical charges?
3. Is there correlation between the number of dependents a patient has and medical charges?
4. Is there correlation between age and medical charges?
5. Do individuals with higher BMI have higher medical charges?


## Analysis

1. What region has the lowest cost of medical care?

![Charges Histogram](https://user-images.githubusercontent.com/112409778/227813514-97acd1b2-554a-4b28-a397-bf3424d2fed6.jpg)

The overall average of charges in the dataset is $13,270.42. However, there is an uneven distribution of charges in the dataset. As indicated in the histogram above there is a right skew that is affecting the average. The median charge, $9,377.90, is a better indication of the amount of a typical medical charge. 


![Region Median Charges ](https://user-images.githubusercontent.com/112409778/227813527-8c016af7-cbef-4218-a31c-87a211c04608.jpg)

The same is true for the distribution of charges in the four regions in the dataset. As aforementioned the median is a better indication of the typical medical charge within each region. The Southwest region has the lowest median charge, $8,798.59, of all the regions in the dataset. This can be attributed to the Southwest region having the least amount of smokers, 58, overall, the least amount of female smokers, 21, in the dataset, and the second smallest amount of male smokers, 37, in the dataset. This is significant due to smokers incurring charges that are four times greater than non-smokers on average!


2. Which  gender has the highest highest typical charges?

The distribution of the charges of both male and females have a right skew in which outliers are impacting the calculation of the average charges. 

![Median Charges Sex](https://user-images.githubusercontent.com/112409778/227813596-335b759e-2ef1-4b87-a8e4-2577365f2c70.jpg)

The median charges of each sex is a better indicator of the typical charges. Males have a median charge of $9,369.62  and females have a median charge of  $9,412.96 as indicated in the bar ch
art above.


3. Is there correlation between the number of dependents a patient has and medical charges?

![Number of Children and Charges Scatter Plot](https://user-images.githubusercontent.com/112409778/227813660-5b866f7b-e106-4894-82db-bb04e728f5fb.jpg)

As indicated in the scatter plot above there is no linear correlation between number of dependents and charges. The correlation coefficient of comparing the number of children a patient has to charges incurred is .07, indicating that there is no correlation. This is also evident in the line of best fit seen on the scatter plot above.


4. Is there correlation between age and medical charges?

![Age and Charges Scatter Plot](https://user-images.githubusercontent.com/112409778/227813708-e345d892-2907-4b04-b49f-41ad5c887c93.jpg)

There is a low correlation between age and charges incurred by patients. This is indicated by the correlation coefficient of 0.30 as well as the line of best fit in the scatter plot above. This is also indicated in the average charges of each age category as well. Teens have an average medical charge of $8,407.35, Adults have an average charge of $10,603.65, Middle Aged Adults have an average medical charge of $15,431.97, and Seniors have an average medical charge of $21,248.02. There is a clear pattern of increased cost as the age of the patient increases.

5. Do individuals with higher BMI have higher medical costs?

![Personal Medical Dashboard (2)](https://user-images.githubusercontent.com/112409778/228240332-e56641f0-ab72-493a-881e-76ea344d7e6f.jpg)


Yes, individuals with higher BMIs have higher medical costs. The higher a patient’s BMI the higher the average charges as indicated in the line chart above. 
