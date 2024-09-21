# Employee Attendance Dashboard

<img src="https://github.com/RadhikaDeshpande1010/Power-BI-Employee-Attendance-Dashboard/blob/main/Visual%20Background.png" height="230" width="1200">

## Table of Contents
* [Introduction](#Introduction)
* [Dashboard Requirements](#Dashboard-Requirements)
* [Dataset](#Dataset)
* [Data Analysis](#Data-Analysis)
* [Data Preparation and Processing](#Q2-Employee-Attendance-Data-Preparation-and-Processing)
* [DAX Formulas Used in Measures](#DAX-Formulas-Used-in-Measures)
* [Dashboard](#Dashboard)
* [Conclusion](#Conclusion)
  
## Introduction
* This project aims to develop a Power BI Dashboard to provide insights into employee attendance patterns within the organization.
* The Power BI dashboard for analyzing employee attendance data can be accessed through the following link: [Employee Attendance Dashboard](https://github.com/RadhikaDeshpande1010/Power-BI-Employee-Attendance-Dashboard/blob/main/SRC/Attendance_Report.pbix)

## Dashboard Requirements
* Primary KPI's - Office Working Days value and Absenteeism rate in the second quarter of 2022.
* Secondary KPI's - Total Attendane, WFH and SL percentage rates in proportion to total available working days in the second quarter of 2022.
* Monthly Trend showing comparison of Attendane, WFH and SL rates over time.
* Table displaying detailed Attendance, WFH and SL percentage rates for day per week.
* Table displaying detailed Attendance, WFH and SL rates information for individual employees.
* Matrix summarizing individual employees data by different dimensions, such as date or week number or month and attendance aliases.

## Dataset
The Q2 Attendance raw data of 2022 year showcased each individual's attendance by date presented in a wide format. Additionally, the dataset provides information like individual's Employee ID, Name and the Attendance aliases (attendance aliases are listed below).
The assigned attendance aliases (attendance key) are as followed:

```
- Present (P) refers to working a full day.
- Leaves refers to not working a full day neither in-office nor out-of-office.
    Here, Absent days include: {PL (PaidLeave), SL (Sick Leave), HPL (Half day PL), HSL (Half day SL), FFL (Floting festival leave), HFFL (Half Day Floting festival leave), BL  (Birthday Leave), LWP (Leave without pay), HLWP (Half day Leave without pay), BRL  (Bereavement Leave), HBRL  (Half Bereavement Leave), WO (Weekly Off), HO (Holiday Off), ML (Menstrual Leave), HML (Half Day ML)}
- WorkFromHome (WFH) refers to working a full day out-of-office and furthermore is not considered absent nor present. (Halfday WorkFromHome is included with WFH during analysis.)
```

## Data Analysis

## Q2 Employee Attendance Data Preparation and Processing 
* Load the Raw Data.
* To conduct the analysis, I needed to convert the dataset from wide to long format. To do so, I used Power Query to unpivot the date columns.
* Data cleaning is performed on Power Query.
* In Power Query, I ensured data quality by removing unnecessary columns, eliminating duplicate rows, and meticulously cleaning individual rows such as correcting spelling mistakes, standardizing formatting, filling in missing values, or resolving conflicting information to ensure to data accuracy and consistency.
* The Q2 attendance data originally did not include the appropriate day of week for each date. To remedy this, I created the column named "Day of Week", which contains the abbreviated  name of the day of the week for each date.
* After Data Preparation and Processing activity, it is ready for developing the Interactive Dashboard.
  
## DAX Formulas Used in Measures

**1. Office Working Days:** This DAX calculates the number of office working days by subtracting non-working days from the total number of days.
* ```
  Office Working Days =
  Var totaldays = [Count]
  VAR nonworkdays = CALCULATE([Count],'Employee_Attendance'[Value] in {"HO", "WO"})
  RETURN
  totaldays-nonworkdays
  ```

**2. Absenteeism  Rate:**  It calculates the percentage of days an employees was absent relative to the total number of office working days.
 * ```
   Absenteeism Rate = DIVIDE([Absent Days],[Office Working Days])
   Here, Absent Days [Value] IN {"PL", "SL", "HPL", "HSL", "FFL", "BL", "LWP", "HLWP", "HFFL", "BRL", "HBRL", "HWFH", "ML", "HML"}
   ```
   
 **3. Attendance Rate:** It represents the percentage of attendance, calculated by dividing the number of days an employee was present by the total number of working days in the office.
 * ```
   Attendance Rate = DIVIDE([Present Days],[Office Working days])
   Here, Present Days [Value] IN {"P", "WFH"}
   ```

 **4. WFH Rate:** It represents WFH ratio or percentage which evaluates the proportion of workdays that employees worked from home compared to the total number of office working days.
 * ```
   WFH Rate = DIVIDE([WFH],[Office Working days])
   ```

 **5. SL Rate:** It represents SL ratio or percentage which evaluates the proportion of sick leave days relative to the total office working days.
 * ```
   SL Rate = DIVIDE([SL],[Office Working days])
   ```

## Dashboard

![Dashboard Image](https://github.com/RadhikaDeshpande1010/Power-BI-Employee-Attendance-Dashboard/blob/main/SRC/Attendance%20Dashboard.png "Attendance Dashboard")

## Conclusion
In conclusion, the Employee Attendance Dashboard has provided valuable insights into our workforce's attendance patterns and behaviors. Through thorough analysis of the data, several key findings have emerged:
* Attendance Rate: Overall, the attendance rate remains high, with the majority of employees consistently attending work as scheduled.
* Absenteeism Trends: While the majority of employees maintain good attendance, there are noticeable trends in absenteeism in the Q2 attendance data of 2022. F Exploring the root causes behind these trends could provide valuable insights for targeted improvement efforts.
* Moreover, the interactive nature of the dashboard empowers users to explore data dynamically and filter information based on their requirements. This fosters a data-driven culture within the organization, facilitating collaboration, transparency, and accountability in managing attendance-related challenges.
* Ultimately, the Employee Attendance Dashboard serves as a central hub for monitoring, analyzing, and optimizing workforce attendance, thereby contributing to the overall efficiency and performance of the organization.
