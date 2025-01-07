# Bellabeat Data Analysis Case Study - Katherine Habura

## Bella Beat Data Analysis Project Introduction
The following is a case study completed as a part of the Google Data Analytics Professional Certificate. The case study uses data provided by the Google Data Analytics Professional Certificate program which was obtained by means of a survey distributed to FitBit users from 03/12/2016-05/12/2016. The data collected from the survey will be used to gain insight into how Bellabeat can become a bigger player in the smart device market, specifically as smart devices apply to women's health. The following questions will be used to guide the analysis: 
* What are some trends in smart device usage?
* How could these trends apply to Bellabeat customers?
* How could these trends help influence Bellabeat marketing strategy? 

My analysis will answer the following overarching question:
* The Bellabeat wellness watch is a product that allows customers to track their activity, sleep, and stress. Is the Bellabeat watch a useful product to women who want to lose weight? What aspect(s) of the Bellabeat watch can be improved upon in order to help Bellabeat customers achieve their weight loss goals?

#### About the Data
The data used for this case study was obtained by means of a survey distributed to FitBit users from 03/12/2016-05/12/2016. The data includes information from 35 unique participants who provided information on their activity levels, sleep, calories ingested, etc. Of the 35 unique survey participants, 13 unique participants were tracking their weight. Of those tracking their weight, only 9 unique participants were tracking their sleep. It is important to note the sample size of this case study as inadequate, and should not be used to make any big decisions for Bellabeat. However, the data from these participants provide enough information for me to showcase my skills in SQL, R, and Google Sheets. 

#### Stakeholders
* Urška Sršen
Bellabeat’s cofounder and Chief Creative Officer
* Sando Mur: 
Mathematician and Bellabeat’s cofounder

***
### **SQL Showcase** <a class="anchor"  id="h1"></a>

#### Leading Question <a class="anchor"  id="h2"></a>
Is there a significant correlation between the amount of times each unique ID logs their weight and their weight loss progress?

#### Data Preparation and Processing with SQL <a class="anchor"  id="h3"></a>
I am curious if those who enter their progress more often show more progress when it comes to weight loss. Therefore, I want to count the number of entries for each unique Id number. I determine their weight loss based on their maximum logged weight and minimum logged weight. Because I want to focus on weight loss, I trim the table to only focus on weight log entries between the minimum entries (2) and maximum entries (44). I save this information as a new table, and then calculate the correlation coefficient.

```sql
-- Upload and trim first data set, remove AM and PM

CREATE TABLE `case-study-432012./kaggle/input/fitbit/mturkfitbit_export_3.12.16-4.11.16/Fitabase Data 3.12.16-4.11.16/weightLogInfo_merged.csv` AS

SELECT
    Id,
    PARSE_DATETIME('%m/%d/%Y %I:%M:%S %p', Date) AS DateTimeOnly,
    WeightPounds,
    BMI
FROM
    `case-study-432012.weight_log_info.weight_log_info1`
ORDER BY
    Id ASC,
    DateTimeOnly ASC;
```
```sql
-- Upload and trim second data set, remove AM and PM

CREATE TABLE `case-study-432012.weight_log_info.weight_log_info2_trimmed` AS

SELECT
    Id,
    PARSE_DATETIME('%m/%d/%Y %I:%M:%S %p', Date) AS DateTimeOnly,
    WeightPounds,
    BMI
FROM
    `case-study-432012.weight_log_info.weight_log_info2`
ORDER BY
    Id ASC,
    DateTimeOnly ASC;
```

```sql
-- Merge first and second data set 

CREATE TABLE `case-study-432012.weight_log_info.merged_weight_log_info` AS

SELECT
  Id,
  DateTimeOnly,
  WeightPounds,
  BMI
FROM 
  `case-study-432012.weight_log_info.weight_log_info1_trimmed`

UNION ALL

SELECT
  Id,
  DateTimeOnly,
  WeightPounds,
  BMI
FROM 
  `case-study-432012.weight_log_info.weight_log_info2_trimmed`
```

#### Data Analysis with SQL <a class="anchor"  id="h3"></a>
I am curious if those who enter their progress more often show more progress when it comes to weight loss. Therefore, I want to count the number of entries for each unique Id number. I determined their weight loss based on their maximum logged weight and minimum logged weight. Because I want to focus on weight loss, I trimed the table to only focus on weight log entries between the minimum entries (2) and maximum entries (44). I saved this information as a new table, and then calculated the correlation coefficient.


```sql
-- Calculate number of entries, min weight, max weight, and weight loss per unique ID

CREATE TABLE `case-study-432012.weight_log_info.merged_weight_log_info4` AS

SELECT 
    Id, 
    CountId,
    Round(MaxWeight, 2) AS MaxWeight,
    Round(MinWeight, 2) AS MinWeight,
    Round(WeightLoss, 2) AS WeightLoss

FROM `case-study-432012.weight_log_info.merged_weight_log_info3`

WHERE 
  CountId BETWEEN 2 AND 44

ORDER BY
    CountId DESC;
```
```sql
-- Calculate correlation coefficient between weight loss and the number of entries per unique ID

SELECT 
  CORR(CountId, WeightLoss),

FROM 
  `case-study-432012.weight_log_info.merged_weight_log_info4`
```

<div align="center">
  <img src="https://i.imgur.com/4KcH9VF.png" width="350">
</div>
<div align="center"> <img src="https://i.imgur.com/kjI1nij.png" width="100">
</div>

With a correlation coefficient of .23, we can conclude that there is not significant correlation between the amount of times each unique ID logs their weight and their weight loss progress.

***
### **Spreadsheets (Google Sheets) Showcase** <a class="anchor"  id="h5"></a>

#### Leading Questions <a class="anchor"  id="h6"></a>
* Is there a significant correlation between the average amount of sleep each unique ID logs and their weight loss progress?

* Is there a significant correlation between the average amount of ingested calories each unique ID logs and their weight loss progress?

* Is there a signfiicant correlation between the average amount of steps each unique ID logs and their weight loss progress? 

* Is there a significant correlation between the average amount of each type of active minutes logged and their weight loss progress?

* Is there a significant correlation between the average amount of total active minutes logged and their weight loss progress?

#### Data Preparation and Processing with Spreadsheets <a class="anchor"  id="h7"></a>
Using the data provided, I sorted, filtered, used v-lookup, etc... 

<div align="center">
  <img src="https://i.imgur.com/ianeY6I.png" width="650">
</div>

Additionally, I was only interested in analyzing the data from those who were logging their weight more than one time, as those would be the clients showing weight change. 

<div align="center">
  <img src="https://i.imgur.com/fpMn11U.png" width="650">
</div>

#### Data Analysis with Spreadsheets <a class="anchor"  id="h8"></a>
In order to decide which products Bellabeat should focus on improving or advertising more often, I look at the correlation between weight loss and 8 different variables - each recorded on a daily basis: Sleep, average amount of calories ingested, average steps, average sedentary minutes, average lightly intense exercise minutes, average fairly intense exercise minutes, average very intense exercise minutes, and the average amount of exercise minutes total (light, fair, and very). Sleep as a variable is recorded in a seperate table so as to include only the unique users who are recording sleep and weight loss. The correlation between weight loss and the other 7 variables are recorded in a table so as only to include on the unique users who are recording these variables and weight loss.

<div align="center">
  <img src="https://i.imgur.com/fX8zySS.png" width="250">
</div>
<div align="center">
  <img src="https://i.imgur.com/kbp1zV6.png" width="850">
</div>

As we can see from the correlation coefficients, it is more important to focus on active minutes than it is to focus on sleep, steps, or ingested calories. We can look at visuals comparing each variable using R in the following section.

***
### **R Showcase - Visuals** <a class="anchor"  id="h9"></a>

#### Leading Questions <a class="anchor"  id="h10"></a>
Using these results, what product(s) should Bellabeat focus on advertising in order to promote weight loss among those who are tracking their weight?

#### Data Visuals with R <a class="anchor"  id="h11"></a>
In order to further show the stakeholders which factors to consider or not consider when promoting weight loss, I created 8 different scatter plots that each include a line of best fit - below. The code used to create one plot and a compilation of all 8 plots in R is also shown below. These scatter plots show the correlation (or lack of correlation) between these factors and weight loss, confirming the weak correlation coefficients calculated in the previous section.

<div align="center">
  <img src="https://i.imgur.com/SR43QeA.png" width="1000">
</div>

```R
plot_1 = ggplot(data = Case_Study, aes(x = Weight_Change, y = Average_Calories_Ingested)) +
  geom_point(color = "darkgreen") +
  geom_smooth(method = "lm", se = FALSE, col = "pink") +
  labs(title = "",
       x = "",
       y = "Avg Calories In")

grid.arrange(
  plot_1,
  plot_2,
  plot_3,
  plot_4,
  plot_5,
  plot_6,
  plot_7,
  plot_8,
  top = "Weight Change Vs...",
  nrow=2
  )
```

## Conclusion
The Bellabeat wellness watch is a product that allows customers to track their activity, sleep, and stress. With this data, one can conclude that the Bellabeat watch is not a useful product to women who want to lose weight when it comes to tracking sleep, steps, or calories ingested. According to the analysis, daily activity (light and overall) is the best indicator for successful weight loss. Therefore, the Bellabeat wellness watch should be advertised as a product that encourages daily activity.

As stated in the beginning of this case study, the sample size used for this study severely hinders the validity of these results. I am surprised to see that sleep, calories ingested, and steps are not indicators of weight loss, and I am curious if a larger sample size would show otherwise. Please use this case study only as a showcase of my skills with SQL, R, and Google Sheets.
