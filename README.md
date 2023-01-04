# Medical Data Analysis

## Abstract

Dataset of personal medical data of 1,338 patients with a variety of variables that have an affect on the cost of medical services provided. The purpose of the analysis is to analyze the effects of variables on the cost of medical care, e.g. age, gender, region, etc. 

- Access Dataset [HERE](https://www.kaggle.com/datasets/mirichoi0218/insurance) 
  - Dataset Name ***Insurance.CSV*** 

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

1. What region has the highest cost of medical care?
2. Which  gender has the highest average charges?
3. Do patients with dependents  have higher medical costs than patients who don’t have dependents?
4. Do individuals with higher BMI have higher medical costs?

## Analysis

1. What region has the lowest cost of medical care?

![Region Average Cost](https://user-images.githubusercontent.com/112409778/210587954-5f90f59d-c6be-4b50-bdf1-2dc37af65bd5.jpg)

The Southwest region has the lowest average of health care due to the following risk factors associated with charges:

Smoking adversely impacts charges, one average smoker incur greater charges than non smokers. The Southwest has the least amount of female smokers, 21, as well as the least amount of smokers regardless of sex, 58.
Age also affects the amount of the charges of the patient, the older the patient the more the charges on average.The Southwest region has the lowest average charges due to the age distribution of patient population within the Southwest region. The Southwest  region has the lowest middle aged population, as well as the most teens compared to other regions . Also, the southwest region has the least amount of female smokers which also affects medical care charges.


2. Which  gender has the highest average charges?

![Average Charges Sex (1)](https://user-images.githubusercontent.com/112409778/210586929-fc2105e7-28d7-49c5-a58a-08c070664ded.jpg)

On average males have the highest average charges,$13,956.75,compared to females,$12,569.58. This can be attributed to a slightly higher BMI as well as 24% of the males in the dataset being smokers compared to that of just 17% of females within the dataset being smokers.


3. Do patients with dependents have higher medical costs than patients who don’t have dependents?

![Average Charges Per Dependent](https://user-images.githubusercontent.com/112409778/210587658-e24ac9fd-8157-431e-88b1-d82d8b940698.jpg)

There is a correlation between the number of children dependents a patient has and the average charges of the patient irregardless of sex. The more dependents a patient has the higher the average cost.However, there are some outliers with patients that have 5 dependents, but it should be disregarded as the amount of patients with 5 dependents isn’t statistically relevant.  


4. Do individuals with higher BMI have higher medical costs?

![BMI Dashboard (1)](https://user-images.githubusercontent.com/112409778/210587831-de7fa4c2-4996-483e-9ea3-784ae143a1ab.jpg)

Yes, there is a correlation between BMI and average charges. The higher a patient’s BMI the higher the average charges. Additionally, the majority of the patients in the dataset are considered to be obese. 

