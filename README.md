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
