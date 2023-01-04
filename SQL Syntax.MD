~~~SQL 
/*Age Categories*/

WITH AGECAT AS
(SELECT 
  age, region, charges,

  CASE 
  WHEN age < 19 THEN 'Teen'
  WHEN age < 39 THEN 'Adult'
  WHEN age <= 59 THEN 'Middle Aged'
  WHEN age >= 60 THEN 'Senior'
  END AS AgeCategory
FROM `my-data-project-36654.Medical_Insurance_Data.Medical_Data_Analysis`)

SELECT 
  DISTINCT AgeCategory,CEILING(AVG(age) OVER ()) AS AVGDatasetAge, 
  COUNT(*) OVER (PARTITION BY AgeCategory) AS AgeCategoryCount,
  ROUND(AVG(charges) OVER (PARTITION BY AgeCategory),2) AS AvgChargeAge
FROM AGECAT
ORDER BY AvgChargeAge;
~~~

<img width="563" alt="Age_Category_SQL_Result " src="https://user-images.githubusercontent.com/112409778/210599423-d84ac497-b0ff-4128-a896-9e70f06fb514.png">


~~~SQL 
/*Sex charge comparison*/

SELECT 
  DISTINCT sex,COUNT(sex) OVER (PARTITION BY sex) AS GenderCount,ROUND(AVG(bmi) OVER (PARTITION BY sex),2) AS AVGSexBMI,
  ROUND(AVG(age) OVER (PARTITION BY sex),0) AS AVGSexAGE,ROUND(AVG(charges) OVER (PARTITION BY sex),2) AS AVGSexCHARGES,
  COUNT(sex) OVER () AS PatientCount, 
FROM `my-data-project-36654.Medical_Insurance_Data.Medical_Data_Analysis` ;
~~~~

<img width="763" alt="Sex_Avg_Charges_Comp" src="https://user-images.githubusercontent.com/112409778/210599770-866a2bff-db72-4e89-8890-9d6042f7c99d.png">

~~~SQL 
/*Sex smoker comparison*/

SELECT 
  DISTINCT sex, smoker, ROUND(AVG(age) OVER (PARTITION BY sex,smoker),0) AS AVGAgeSmoker,
  COUNT (smoker) OVER (PARTITION BY sex,smoker) AS SmokerSexCount, 
  COUNT (sex) OVER (PARTITION BY sex) AS SexCount,
  ROUND((COUNT (smoker) OVER (PARTITION BY sex,smoker)/COUNT (sex) OVER (PARTITION BY sex) * 100),0) AS SmokerPercentage,
  ROUND(AVG(BMI) OVER (PARTITION BY sex,smoker),2) AS SmokerSexBMI, 
  ROUND(AVG(charges) OVER (PARTITION BY sex,smoker),2) AS AVGChargesSmokers
FROM `my-data-project-36654.Medical_Insurance_Data.Medical_Data_Analysis`
ORDER BY sex;
~~~~

<img width="945" alt="Sex_Somker_Charge_Comp" src="https://user-images.githubusercontent.com/112409778/210600039-478d9c06-4237-4638-8641-42f519bd82b4.png">

~~~SQL
/*Smoker Region Totals*/
SELECT
  DISTINCT region,smoker, COUNT(smoker) OVER (PARTITION BY region, 
  smoker) AS SmokerRegionCount,COUNT(smoker) OVER () AS TotalSmokerCount,
  ROUND((COUNT(smoker) OVER (PARTITION BY region, smoker)/COUNT(smoker) OVER ()*100),0) AS SmokerPercentage
FROM `my-data-project-36654.Medical_Insurance_Data.Medical_Data_Analysis`
WHERE smoker = true
ORDER BY SmokerRegionCount;
~~~

<img width="727" alt="Smoker_Region_Totals" src="https://user-images.githubusercontent.com/112409778/210600453-8562b0a0-1e11-4bfa-8106-c60effcbae42.png">

~~~SQL
/*Female Smokers by Region*/

SELECT
  DISTINCT sex,region,smoker, COUNT(smoker) OVER (PARTITION BY region, sex, smoker) AS SmokerRegionCount,
  COUNT(smoker) OVER () AS SmokerTotal, 
  ROUND((COUNT(smoker) OVER (PARTITION BY region, sex, smoker)/COUNT(smoker) OVER () * 100),0) AS RegionFemaleSmokerPercentage
FROM `my-data-project-36654.Medical_Insurance_Data.Medical_Data_Analysis`
WHERE sex = 'female' AND smoker = true
ORDER BY SmokerRegionCount;
~~~

<img width="871" alt="Female_Region_Smokers" src="https://user-images.githubusercontent.com/112409778/210601062-929f9dd1-402c-445f-9ad2-969d91101ea4.png">


~~~SQL
/*Children charge comparison*/

SELECT 
  DISTINCT children, 
  ROUND(AVG(age) OVER (PARTITION BY children),0) AS AVGParentAGE, 
  ROUND(AVG(charges) OVER (PARTITION BY children),2) AS AVGParentCHARGES, 
  COUNT(*) OVER (PARTITION BY children ) AS ParentCount
FROM `my-data-project-36654.Medical_Insurance_Data.Medical_Data_Analysis`
ORDER BY children;
~~~

<img width="463" alt="Dependent_Charges" src="https://user-images.githubusercontent.com/112409778/210600821-42548a7f-82b1-4ab8-add2-23f89bd93e66.png">

~~~SQL 

/*Region charge comparison*/

SELECT 
  DISTINCT region,sex,COUNT(sex) OVER (PARTITION BY sex, region) AS SexRegionCount,
  COUNT(sex) OVER (PARTITION BY region) AS RegionPop,
  ROUND((COUNT(sex) OVER (PARTITION BY sex, region)/COUNT(sex) OVER (PARTITION BY region)* 100),1) AS SexPercentage,
  ROUND(AVG(charges) OVER (PARTITION BY sex,region),2) AS RegionSexChargesAVG,
  ROUND(AVG(charges) OVER (PARTITION BY region),2) AS RegionAVGCost,
  ROUND(AVG(BMI) OVER (PARTITION BY region,sex),2) AS AVGBMI
FROM `my-data-project-36654.Medical_Insurance_Data.Medical_Data_Analysis`
ORDER BY RegionAVGCost ;
~~~

<img width="1065" alt="Region_avg_Cost" src="https://user-images.githubusercontent.com/112409778/210601379-8bff3685-3d17-497b-a179-24d31fd1bc17.png">


~~~SQL
/*Average Charges by BMI Categories*/

WITH BMI AS (
SELECT 
    CASE
    WHEN bmi < 18.5 THEN 'Underweight'
    WHEN  bmi BETWEEN 18.5 AND 24.9 THEN 'Normal'
    WHEN bmi < 30 THEN 'Overweight'
    WHEN bmi >= 30.0 THEN 'Obese'
    END AS BMICategory,

  bmi,charges
FROM `my-data-project-36654.Medical_Insurance_Data.Medical_Data_Analysis`
ORDER BY bmi)

SELECT 
  DISTINCT bmicategory,ROUND(AVG(charges) OVER (PARTITION BY bmicategory),2) AS AVGChargesBMI, 
  COUNT(*) OVER (PARTITION BY bmicategory) AS CategoryCount
FROM BMI
ORDER BY AVGChargesBMI;
~~~

<img width="456" alt="BMI_Categories" src="https://user-images.githubusercontent.com/112409778/210601721-0aa29235-3e37-4e29-979f-6703b1fcd2da.png">
