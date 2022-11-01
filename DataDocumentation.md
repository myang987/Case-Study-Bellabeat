### 21/10/2022 - Upload and change data format
- All tables were cleaned and uploaded into a new table 
- Tables 5-18 had timestamps uploaded as STRING then formatted and converted to DateTime in a new column.
- Old STRING format timestamp column was removed in the new table

### Change fitbit data table names:
**01. dailyActivity_merged -> Daily_Activity** <br />
Verified: done
Number of Users: 33

**02. dailyCalories_merged - > Daily_Calories** <br />
Verified: done
Number of Users: 33

**03. dailyIntensities_merged -> Daily_Intensities** <br />
Verified: done
Number of Users: 33

**04. dailySteps_merged -> Daily_Steps** <br />
Verified: done
Number of Users: 33

**05. heartrate_seconds_merged -> Heartrate_Seconds** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 14

&emsp;**IDs that do not appear in Daily_Activity** <br />
&emsp;8053475328	1644430081	4319703577	2320127002	1503960366 <br />
&emsp;3372868164	7086361926	2873212765	6290855005	4445114986 <br />
&emsp;8378563200	8583815059	1927972279	4057192912	3977333714 <br />
&emsp;4702921684	1844505072	1624580081	8253242879 <br />

**06. hourlyCalories_merged -> Hourly_Calories** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**07. hourlyIntensities_merged -> Hourly_Intensities** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**08. hourlySteps_merged -> Hourly_Steps** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**09. minuteCaloriesNarrow_merged -> Calories_per_Minute_Narrow** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**10. minuteCaloriesWide_merged -> Calories_per_Minute_Wide** <br />
Uploaded: ActivityHour as string
Verified: done
Number of Users: 33

**11. minuteIntensitiesNarrow_merged -> Intensities_per_Minute_Narrow** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**12. minuteIntensitiesWide_merged -> Intensities_per_Minute_Wide** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**13. minuteMETsNarrow_merged -> METs_per_Minute_Narrow** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**14. minuteSleep_merged -> Minute_Sleep** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 24

&emsp;**IDs that do not appear in Daily_Activity** <br />
&emsp;8877689391	3372868164	2873212765	6290855005	8583815059 <br />
&emsp;2022484408	4057192912	1624580081	8253242879 <br />

**15. minuteStepsNarrow_merged -> Steps_per_Minute_Narrow** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**16. minuteStepsWide_merged -> Steps_per_Minute_Wide** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 33

**17. sleepDay_merged -> Sleep_per_Day** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 24

&emsp;**IDs that do not appear in Daily_Activity** <br />
&emsp;8877689391	3372868164	2873212765	6290855005	8583815059 <br />
&emsp;2022484408	4057192912	1624580081	8253242879 <br />


**18. weightLogInfo_merged -> Weight_Log_Info** <br />
Uploaded: datetime as string
Verified: done
Number of Users: 8

&emsp;**IDs that do not appear in Daily_Activity** <br />
&emsp;8053475328	1644430081	2320127002	2347167796	4388161847 <br />
&emsp;6775888955	5553957443	3372868164	7086361926	6290855005 <br />
&emsp;4445114986	4020332650	6117666160	8378563200	8583815059 <br />
&emsp;2026352035	7007744171	2022484408	8792009665	4057192912 <br />
&emsp;3977333714	4702921684	1844505072	1624580081	8253242879 <br />

### 27/10/2022 - Merge and transform fitbit data into new tables for analysis

**1. Sleep_Time** <br />
Querys: #10, #11

**2. Hourly_Activity** <br />
Querys: #14

**3. Heartrate_by_Hour** <br />
Querys: #18

**4. Daily_Activity_Avg_by_Week** <br />

**5. Avg_Heartrate_per_Minute** <br />

**6. Avg_Activity_per_Hour** <br />

The use of transformed datasets were abandoned. The creation of altered and merged tables were conducted in Tableau using the cleaned dataset. 
