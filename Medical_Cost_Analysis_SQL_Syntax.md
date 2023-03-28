~~~ SQL
/*Age Categories*/

CREATE TEMP TABLE AGECAT AS -- Creating TEMP TABLE AGECAT
SELECT 
  age, region, charges,

  CASE 
  WHEN age <= 19 THEN 'Teen'
  WHEN age BETWEEN 20 AND 39 THEN 'Adult'
  WHEN age BETWEEN 40 AND 59 THEN 'Middle Age'
  WHEN age >= 60 THEN 'Senior'
  END AS AgeCategory
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`;

~~~

~~~ SQL 
/*Age Category Averages*/
SELECT 
  DISTINCT AgeCategory, 
  COUNT(*) OVER (PARTITION BY AgeCategory) AS AgeCategoryCount,
  ROUND(AVG(charges) OVER (PARTITION BY AgeCategory),2) AS AvgChargeAge
FROM AGECAT
ORDER BY AvgChargeAge;
~~~

**Result**

|AgeCategory|AgeCategoryCount|AvgChargeAge|
|---|---|---|
|Teen|137|8407.35|
|Adult|537|10603.65|
|Middle Age|550|15431.97|
|Senior|114|21248.02|


~~~ SQL 
/*Correlation Between Age and Charges*/
SELECT
  ROUND(CORR(Age,charges),2) AS CORR_Age_Charges
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`;
-- Low correlation between age and charges 
~~~

**Result**

|CORR_Age_Charges|
|---|
|0.30|

~~~ SQL 
/*Distribution of Charges*/
SELECT 
  DISTINCT TRUNC(charges,-3) AS Charge_Bin, 
  COUNT(*) AS Count
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`
GROUP BY Charge_Bin
ORDER BY Charge_Bin;
--Right skew of distribution
~~~

**Result**
|Charge_Bin|Count|
|---|---|
|0.0|712|
|10000.0|353|
|20000.0|111|
|30000.0|83|
|40000.0|72|
|50000.0|4|
|60000.0|3|

~~~ SQL
/*Male Distrubution of Charges*/
SELECT  
  DISTINCT sex,
  TRUNC(charges,-4) AS charge_bins,
  COUNT(*) AS Count
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`
WHERE Sex = 'male'
GROUP BY sex,charge_bins
ORDER BY charge_bins;
--Right skew
~~~

**Result**

|sex|charge_bins|count|
|---|---|---|
|male|0.0|357|
|male|10000.0|161|
|male|20000.0|55|
|male|30000.0|56|
|male|40000.0|43|
|male|50000.0|2|
|male|60000.0|2|

~~~ SQL 
/*Female Distribution of Charges*/
SELECT  
  DISTINCT sex,
  TRUNC(charges,-4) AS charge_bins,
  COUNT(*)
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`
WHERE Sex = 'female'
GROUP BY sex,charge_bins
ORDER BY charge_bins;
-- Right skew
~~~

**Result**
|sex|charge_bins|Count|
|---|---|---|
|female|0.0|355|
|female|10000.0|192|
|female|20000.0|56|
|female|30000.0	|27|
|female|40000.0|29|
|female|50000.0|2|
|female|60000.0|1|

~~~ SQL 
/*Male and Female Average Charges*/
SELECT 
  DISTINCT Sex, 
  ROUND(AVG(charges) OVER (PARTITION BY sex),2) AS Avg_Charges_Sex
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`;
~~~

**Result**

|Sex|Avg_Charges_Sex|
|---|---|
|male|13956.75|
|female|12569.58|

~~~ SQL 
/*Male and Female Median Charges*/
SELECT 
  DISTINCT Sex,
  ROUND(PERCENTILE_CONT(charges, 0.50) OVER (PARTITION BY Sex),2) AS Sex_Median
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`;
~~~

**Result**

|Sex|Sex_Median|
|---|---|
|male|9369.62|
|female|9412.96|

~~~ SQL 
/*Smoker Region Totals*/
SELECT
  DISTINCT region,smoker, COUNT(smoker) OVER (PARTITION BY region, 
  smoker) AS SmokerRegionCount,COUNT(smoker) OVER () AS TotalSmokerCount,
  ROUND((COUNT(smoker) OVER (PARTITION BY region, smoker)/COUNT(smoker) OVER ()*100),0) AS SmokerPercentage
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`
WHERE smoker = true
ORDER BY SmokerRegionCount;
--Southwest has the least amount of smokers
~~~

**Result**

|region|smoker|SmokerRegionCount|TotalSmokerCount|SmokerPercentage|
|---|---|---|---|---|
|northwest|true|58|274|21.0|
|southwest|true|58|274|21.0|
|northeast|true|67|274|24.0|
|southeast|true|91|274|33.0|

~~~ SQL
SELECT
  Smoker, 
  ROUND(AVG(charges),2) AS Avg_Smoking_Charges
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`
GROUP BY Smoker;
~~~
**Result**

|Smoker|Avg_Smoking_Charges|
|---|---|
|false|8434.27|
|true|32050.23|

~~~ SQL
/*Comparing charges for smokers to non-smokers*/
SELECT
  ROUND(32050.23/8434.27);
--smoking accounts for an average cost that is about four times greater than a non-smoker
~~~

**Result**
|Smoker_Non_Smoker_Comparsion|
|---|
|4.0|

~~~ SQL
/*Smokers by Region - Sex*/
SELECT
  DISTINCT sex,region,smoker, COUNT(smoker) OVER (PARTITION BY region, sex, smoker) AS SmokerRegionCount,
  COUNT(smoker) OVER () AS SmokerTotal, 
  ROUND((COUNT(smoker) OVER (PARTITION BY region, sex, smoker)/COUNT(smoker) OVER () * 100),0) AS RegionFemaleSmokerPercentage
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`
WHERE smoker = true
ORDER BY SmokerRegionCount;
--Southwest has lowest number of female smokers
~~~

**Result**
|sex|region|smoker|SmokerRegionCount|SmokerTotal|RegionSexSmokerPercentage|
|---|---|---|---|---|---|
|female|southwest|true|21|274|8.0|
|female|northwest|true|29|274|11.0|
|female|northeast|true|29|274|11.0|
|male|northwest|true|29|274|11.0|
|female|southeast|true|36|274|13.0|
|male|southwest|true|37|274|14.0|
|male|northeast|true|38|274|14.0|
male|southeast|true|55|274|20.0|

~~~ SQL 
/*Children and Charge Correlation*/
SELECT 
  ROUND(CORR(children, charges),2) AS CORR_CO_Charges
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`;
~~~

**Result**
|CORR_CO_Charges|
|---|
|0.07|

~~~ SQL 
/*Region Median Charges*/
SELECT 
   DISTINCT Region,
   ROUND(PERCENTILE_CONT(charges, 0.50) OVER (PARTITION BY Region),2) AS Region_Median,
  ROUND(PERCENTILE_CONT(charges, 0.50) OVER (),2) AS Overall_Median
FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`
ORDER BY Region_Median;
~~~

**Result**
|Region|Region_Median|Overall_Median|
|---|---|---|
|southwest|8798.59|9382.03|
|northwest|8965.80|9382.03|
|southeast|9294.13|9382.03|
|northeast|10057.65|9382.03|


~~~ SQL 
/*BMI Categories*/
CREATE TEMP TABLE BMI_Table AS
SELECT 
*,
  CASE 
  WHEN BMI < 18.5 THEN 'Underweight'
  WHEN BMI >= 18.5 AND BMI < 25 THEN 'Normal'
  WHEN BMI >= 25 AND BMI < 30 THEN 'Overweight'
  WHEN BMI >= 30 THEN 'Obese'
  END AS BMI_Category,

  CASE 
  WHEN BMI < 30 THEN 'Not Obese'
  WHEN BMI >= 30 THEN 'Obese'
  END Obese

FROM `single-being-353600.Medical_Insurance_Data.Insurance_Data`;

SELECT 
  BMI_Category,
  ROUND(AVG(charges),2) AS Avg_Cost
FROM BMI_Table
GROUP BY BMI_Category
ORDER BY Avg_Cost;
~~~

~~~ SQL 
SELECT 
  BMI_Category,
  ROUND(AVG(charges),2) AS Avg_Cost
FROM BMI_Table
GROUP BY BMI_Category
ORDER BY Avg_Cost;
~~~
**Result**

|BMI_Category|Avg_Cost|
|---|---|
|Underweight|8852.2|
|Normal|10409.34|
|Overweight|10987.51|
|Obese|15552.34|

~~~ SQL 
/Calculating Avg and Median Charges of BMI Subgroups*/
SELECT 
  DISTINCT Obese,
  ROUND(AVG(charges) OVER (PARTITION BY Obese),2) AS Avg_Charges_Obese,
  PERCENTILE_DISC(charges,0.50) OVER (PARTITION BY Obese) AS Obese_Category_Median
FROM BMI_Table
WHERE Smoker IS TRUE
~~~

**Result**

|Obese|Avg_Charges_Obese|Obese_Category_Median|
|---|---|---|
|Not Obese|21363.22|20167.34|
|Obese|41557.99|40904.2|
