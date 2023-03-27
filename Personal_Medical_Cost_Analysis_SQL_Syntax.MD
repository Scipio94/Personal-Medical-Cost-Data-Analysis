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
