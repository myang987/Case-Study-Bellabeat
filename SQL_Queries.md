### #1 Copy existing table into a new group
```sql
CREATE TABLE bellabeat-362202.Fitbit_Cleaned.Daily_Steps AS (
    SELECT
    *
  FROM
    bellabeat-362202.fitbit.dailySteps_merged
  )
``` 

### #2 Splitting the date values and formatting from String to correct data type From “MM/DD/YYYY HH/MM/SS A(P)M” as STRING into separate “YYYY/MM/DD” and “HH/MM/SS” and “AM” or “PM” indicator
```sql
SELECT
  DISTINCT CAST(SPLIT(Time, ' ')[offset(0)] as DATE FORMAT 'MM/DD/YYYY') as Date,
  CAST(SPLIT(Time, ' ')[offset(1)] as TIME ) as HMS,
  SPLIT(Time, ' ')[offset(2)] as Time_Of_Day
FROM
  bellabeat-362202.FitBit_Fitness_Tracker.Heartrate_Seconds
```
 
### #3 Convert ‘m/d/Y H:M:S AM’ string to ‘Y-m-d H:M:S’ datetime
```sql
SELECT
  CAST(
      PARSE_TIMESTAMP('%m/%d/%Y %I:%M:%S %p', date_string_column) 
      AS datetime ) AS new_column_name
FROM
  Dataset.name
```

### #4 Write the formatted datetime column into a new dataset
```sql
CREATE TABLE bellabeat-362202.Fitbit_Cleaned.Weight_Log_Info AS (
    SELECT
    *,
    CAST(
      PARSE_TIMESTAMP('%m/%d/%Y %I:%M:%S %p', Date) 
      AS datetime ) AS Datetime
  FROM
    bellabeat-362202.fitbit.weightLogInfo_merged
  );
```

### #5 Remove the old date column from the new table
```sql
ALTER TABLE bellabeat-362202.Fitbit_Cleaned.Weight_Log_Info
DROP COLUMN Date;
```

### #6 View average activity distance and minutes by day of the week
```sql
SELECT
  FORMAT_TIMESTAMP('%A', ActivityDate) AS Day,
  ROUND(avg(Calories), 2) AS avg_calories,
  ROUND(avg(TotalSteps), 2) AS avg_total_steps,
  ROUND(avg(TotalDistance), 2) AS avg_total_distance,
  ROUND(avg(TrackerDistance), 2) AS avg_tracker_distance,
  ROUND(avg(LoggedActivitiesDistance), 2) AS avg_logged_act_distance,
  ROUND(avg(SedentaryActiveDistance), 5) AS avg_sedAct_distance,
  ROUND(avg(LightActiveDistance), 3) AS avg_lightAct_distance,
  ROUND(avg(ModeratelyActiveDistance), 3) AS avg_modAct_distance,
  ROUND(avg(VeryActiveDistance), 3) AS avg_veryAct_distance,
  ROUND(avg(SedentaryMinutes), 2) AS avg_sedAct_minutes,
  ROUND(avg(LightlyActiveMinutes), 2) AS avg_lightAct_minutes,
  ROUND(avg(FairlyActiveMinutes), 2) AS avg_modAct_minutes,
  ROUND(avg(VeryActiveMinutes), 2) AS avg_veryAct_minutes
FROM
  bellabeat-362202.Fitbit_Cleaned.Daily_Activity
GROUP BY
  Day
ORDER BY (
  CASE Day
  WHEN 'Monday'     THEN 0 
  WHEN 'Tuesday'    THEN 1
  WHEN 'Wednesday'  THEN 2 
  WHEN 'Thursday'   THEN 3 
  WHEN 'Friday'     THEN 4 
  WHEN 'Saturday'   THEN 5 
  WHEN 'Sunday'     THEN 6 
  END
) ASC
``` 
 
### #7 Count amount of unique IDs
```sql
SELECT COUNT(DISTINCT Id) AS Num_Of_Users
FROM table.name
```

### #8 Show unique IDs that do not appear in both tables
```sql
(
  SELECT Id FROM table1
  EXCEPT DISTINCT
  SELECT Id from table2
)
 
UNION ALL
 
(
  SELECT Id FROM table2
  EXCEPT DISTINCT
  SELECT Id from table1
)
```

### #9 Display max/min of a column and day
```sql
( 
SELECT
  Day,
  Column AS newName
FROM 
  dataTable
WHERE
  avg_calories = (SELECT max(avg_calories) from dataTable)
)
UNION ALL
( 
SELECT
  Day,
  Column AS newName
FROM 
  dataTable
WHERE
  avg_calories = (SELECT min(avg_calories) from dataTable)
)
 
-- avg_calories             | max: Tue | min: Thur
-- avg_total_steps          | max: Sat | min: Sun
-- avg_total_distance       | max: Sat | min: Sun
-- avg_tracker_distance     | max: Sat | min: Sun 
-- avg_logged_act_distance  | max: Mon | min: Sat/Sun
-- avg_sedAct_distance      | max: Mon | min: Sun
-- avg_lightAct_distance    | max: Sat | min: Sun
-- avg_modAct_distance      | max: Sat | min: Fri
-- avg_veryAct_distance     | max: Wed | min: Fri
-- avg_sedAct_minutes       | max: Mon | min: Thur
-- avg_lightAct_minutes     | max: Sat | min: Sun
-- avg_modAct_minutes       | max: Thur | min: Sat
-- avg_veryAct_minutes      | max: Mon | min: Thurs
```

### #10 Extract daily sleep start time and end time from Minute_Sleep
```sql
SELECT
  Id,
  logId,
  EXTRACT(DATE from min(Datetime)) AS Day,
  EXTRACT(TIME from min(Datetime)) AS sleep_start,
  EXTRACT(TIME from max(Datetime)) AS sleep_end
FROM
  bellabeat-362202.Fitbit_Cleaned.Minute_Sleep
GROUP BY
  Id, logId
```

### #11 Merge Sleep_per_Day and the result from above to aggregate daily sleep and sleep time
```sql
SELECT 
  day.Id,
  time.logId,
  time.Day,
  TotalSleepRecords,
  TotalMinutesAsleep,
  TotalTimeInBed,
  sleep_start,
  sleep_end
FROM 
  bellabeat-362202.Fitbit_Cleaned.Sleep_per_Day AS day
INNER JOIN
  bellabeat-362202.Analysis.Sleep_Time AS time
ON day.Id = time.Id AND
    EXTRACT(DATE from day.Datetime) = TIME.Day
```

### #12 Two queries above together
```sql
SELECT 
  day.Id,
  time.logId,
  time.Day,
  TotalSleepRecords,
  TotalMinutesAsleep,
  TotalTimeInBed,
  sleep_start,
  sleep_end
FROM 
  bellabeat-362202.Fitbit_Cleaned.Sleep_per_Day AS day
INNER JOIN
  (SELECT
    Id,
    logId,
    EXTRACT(DATE from min(Datetime)) AS Day,
    EXTRACT(TIME from min(Datetime)) AS sleep_start,
    EXTRACT(TIME from max(Datetime)) AS sleep_end
  FROM
    bellabeat-362202.Fitbit_Cleaned.Minute_Sleep
  GROUP BY
    Id, logId
  ) AS time
ON day.Id = time.Id AND
    EXTRACT(DATE from day.Datetime) = TIME.Day
```

### #13 Avg time asleep and in bed by day of week
```sql
SELECT
  FORMAT_TIMESTAMP('%A', Day) AS Day,
  ROUND(avg(TotalMinutesAsleep), 0) AS avg_time_asleep,
  ROUND(avg(TotalTimeInBed), 0) AS avg_time_in_bed
FROM
  bellabeat-362202.Analysis.Sleep_Time
GROUP BY
  Day
ORDER BY (
  CASE Day
  WHEN 'Monday'     THEN 0 
  WHEN 'Tuesday'    THEN 1
  WHEN 'Wednesday'  THEN 2 
  WHEN 'Thursday'   THEN 3 
  WHEN 'Friday'     THEN 4 
  WHEN 'Saturday'   THEN 5 
  WHEN 'Sunday'     THEN 6 
  END
) ASC
```

### #14 Merge Hourly Calorie, Steps, and Intensity
```sql
SELECT
  C.Id,
  C.Datetime,
  StepTotal AS Steps,
  Calories,
  TotalIntensity AS Total_Intensity,
  AverageIntensity AS Avg_Intensity
FROM
  bellabeat-362202.Fitbit_Cleaned.Hourly_Calories AS C
  JOIN
  bellabeat-362202.Fitbit_Cleaned.Hourly_Intensities AS I
  ON
  C.Id = I.Id AND
  C.Datetime = I.Datetime
  JOIN
  bellabeat-362202.Fitbit_Cleaned.Hourly_Steps AS S
  ON
  C.Id = S.Id AND
  C.Datetime = S.Datetime
ORDER BY
  Id, Datetime
```

### #15 Average activity per hour of day
```sql
SELECT 
  EXTRACT(Hour from Datetime) AS Hour,
  avg(Steps) AS Avg_Steps,
  avg(Calories) AS Avg_Calories,
  avg(Total_Intensity) AS Avg_Total_Intensity,
  avg(Avg_Intensity) AS Avg_Intensity_per_Min
FROM
  bellabeat-362202.Analysis.Hourly_Activity
GROUP BY
  Hour
```

### #16 Aggregating heartrate per second to average heartrate per minute
```sql
SELECT
  Id,
  DATE_TRUNC(Datetime, minute) AS Timestamp,
  avg(Value) AS Avg_Heartrate
FROM
  bellabeat-362202.Fitbit_Cleaned.Heartrate_Seconds
GROUP BY
  Id, Timestamp
```

### #17 Merge narrow heartrate, calorie, intensity, and METs per minute tables
```sql
SELECT
  tb1.Id,
  Timestamp,
  Avg_Heartrate,
  Calories,
  Intensity,
  METs
FROM
  bellabeat-362202.Analysis.Avg_Heartrate_per_Minute as tb1
  INNER JOIN bellabeat-362202.Fitbit_Cleaned.Calories_per_Minute_Narrow as tb2
  ON tb1.Id = tb2.Id AND tb1.Timestamp = tb2.Datetime
  INNER JOIN bellabeat-362202.Fitbit_Cleaned.Intensity_per_Minute_Narrow as tb3
  ON tb1.Id = tb3.Id AND tb1.Timestamp = tb3.Datetime
  INNER JOIN bellabeat-362202.Fitbit_Cleaned.METs_per_Minute_Narrow as tb4
  ON tb1.Id = tb4.Id AND tb1.Timestamp = tb4.Datetime
ORDER BY
  tb1.Id, Timestamp asc
```

### #18 Calculating average heartrate by the hour of day
```sql
SELECT
  EXTRACT(Hour from Timestamp) AS Hour_of_Day,
  avg(Avg_Heartrate) as Avg_Heartrate
FROM
  bellabeat-362202.Analysis.Avg_Heartrate_per_Minute
GROUP BY
  Hour_of_Day
ORDER BY
  Hour_of_Day
 ```
