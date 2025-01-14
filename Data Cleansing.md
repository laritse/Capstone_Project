## DATA EXPLORATION AND CLEANING USING BIGQUERY

Datasets were on different tables, appending tables together using "UNION ALL" statement and excluding columns 

```sql

CREATE TABLE divvy_tripdata_2023.combined_tripsV1 as (
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Jan_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Feb_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Mar_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Apr_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.May_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.May_2023_2ndhalf
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.June_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.June_2023_2ndhalf
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.July_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.July_2023_2ndhalf
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Aug_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Aug_2023_2ndhalf
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Sept_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Sept_2023_2ndhalf
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Oct_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Oct_2023_2ndhalf
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Nov_2023
UNION ALL
SELECT *
EXCEPT (start_station_id, end_station_id)
FROM liquid-cumulus-411017.divvy_tripdata_2023.Dec_2023
ORDER BY 3)

```


Checking for duplicates in the ride_id column
```sql

SELECT
ride_id,COUNT(*) num_of_dupl
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV1
GROUP BY ride_id
HAVING COUNT(*)>1
-- a total of 400900 ride ID duplicates were discovered
```

Discovered test trips in the data, these will be deleted as they are irrelevant for analysis
```sql

DELETE 
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV1
WHERE 
start_station_name = 'Base - 2132 W Hubbard' OR
start_station_name = 'OH - BONFIRE - TESTING' OR
start_station_name = 'OH Charging Stx - Test' OR
start_station_name = '410' OR
end_station_name = 'Base - 2132 W Hubbard' OR
end_station_name = 'OH - BONFIRE - TESTING' OR
end_station_name = 'OH Charging Stx - Test' OR
end_station_name = '410'

```
Discovered a large number of null values in the data, mostly station names and lng and lat columns. 
checking the number of null values in both the lng and lat columns. In total there are 7346

```sql

SELECT 
COUNT (*)
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV1
WHERE start_lat IS NULL OR start_lng IS NULL OR end_lat IS NULL OR end_lng IS NULL

```

Checking the number of null values in both start and end stations. A total of 1423176 rows with null values exist. 
Deleting this much rows will skew the data, therefore both columns will be ignored/removed in order to prevent the appearance of null values in analysis. 
Considering lng and lat columns have a lower existence of null values, these rows (null values) will be deleted and columns used for analysis.

```sql

SELECT 
COUNT (*)
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV1
WHERE start_station_name IS NULL OR end_station_name IS NULL

-- cleaning table and saving same as new table for further cleaning 
CREATE TABLE divvy_tripdata_2023.combined_tripsV02 as (
SELECT
distinct ride_id,-- removing duplicate ID rows discovered
rideable_type,
-- standardizing date and time formats
EXTRACT (DATE FROM started_at) start_date,
EXTRACT (TIME FROM started_at) start_time,
EXTRACT (DATE FROM ended_at) end_date,
EXTRACT (TIME FROM ended_at) end_time,
-- creating a trip duration column 
TIMESTAMP_DIFF(ended_at, started_at, MINUTE) AS duration,
--creating a new column representing each day of week from the started_at column
FORMAT_DATE('%A', started_at) day_of_week,
FORMAT_DATE('%B', started_at) month,
--creating a column representing each month season from the started_at column
CASE WHEN FORMAT_DATE('%B', started_at) = 'January' THEN 'Winter'
     WHEN FORMAT_DATE('%B', started_at) = 'February' THEN 'Winter'
     WHEN FORMAT_DATE('%B', started_at) = 'March' THEN 'Spring'
     WHEN FORMAT_DATE('%B', started_at) = 'April' THEN 'Spring'
     WHEN FORMAT_DATE('%B', started_at) = 'May' THEN 'Spring'
     WHEN FORMAT_DATE('%B', started_at) = 'June' THEN 'Summer'
     WHEN FORMAT_DATE('%B', started_at) = 'July' THEN 'Summer'
     WHEN FORMAT_DATE('%B', started_at) = 'August' THEN 'Summer'
     WHEN FORMAT_DATE('%B', started_at) = 'September' THEN 'Autumn'
     WHEN FORMAT_DATE('%B', started_at) = 'October' THEN 'Autumn'
     WHEN FORMAT_DATE('%B', started_at) = 'November' THEN 'Autumn'  
     WHEN FORMAT_DATE('%B', started_at) = 'December' THEN 'Winter'
     END AS season, 
start_lat,
start_lng,
end_lat,
end_lng,
member_casual
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV1
ORDER BY 3,4)

```

Deleting rows with null values
```sql

DELETE
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
WHERE ride_id IS NULL OR rideable_type IS NULL OR start_date IS NULL OR end_date IS NULL OR start_lat IS NULL OR start_lng IS NULL OR end_lat IS NULL
OR end_lng IS NULL OR member_casual IS NULL

```

Ride type "docked_bike" appears to be a naming error as the allowable rideable_types are "classic" and "electric" bikes. 
considering the fact that classic bikes are required to be docked at stations, in this instance, 
this may have resulted in the naming error, therefore all records with same naming error will be replaced with classic bikes 

```sql

UPDATE liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
SET rideable_type = 'classic_bike'
WHERE rideable_type = 'docked_bike'
-- the statement modified 76,120 rows
```

Updating rideable_type names with the appropriate case and removal of special character (underscore) from same

```sql
UPDATE liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
SET rideable_type = 'Classic bike'
WHERE rideable_type = 'classic_bike'
-- the statement modified 2,641,292 rows
```

```sql

UPDATE liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
SET rideable_type = 'Electric bike'
WHERE rideable_type = 'electric_bike'
-- the statement modified 2,819,816 rows

```

Removing trips below 1 minute as this could be false starts or user attempt to re-dock bike 

```sql

DELETE
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
WHERE duration < 1 
-- the statement removed 104,829 rows

```

 ## ANALYSIS 
Number of rides by time of day and day of week as per bike and member type 

```sql

SELECT
rideable_type,
member_casual,
day_of_week,
COUNT(*) number_of_rides,
EXTRACT(HOUR FROM start_time) time_of_day
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
GROUP BY rideable_type, member_casual, time_of_day, day_of_week
ORDER BY time_of_day,
CASE
          WHEN day_of_week = 'Sunday' THEN 1
          WHEN day_of_week = 'Monday' THEN 2
          WHEN day_of_week = 'Tuesday' THEN 3
          WHEN day_of_week = 'Wednesday' THEN 4
          WHEN day_of_week = 'Thursday' THEN 5
          WHEN day_of_week = 'Friday' THEN 6
          WHEN day_of_week = 'Saturday' THEN 7
     END ASC

```


Average length of ride per day

```sql

SELECT
member_casual,
day_of_week,
ROUND(AVG(duration)) AS avg_ride_time,
FROM  liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
GROUP BY member_casual, day_of_week
ORDER BY  CASE
          WHEN day_of_week = 'Sunday' THEN 1
          WHEN day_of_week = 'Monday' THEN 2
          WHEN day_of_week = 'Tuesday' THEN 3
          WHEN day_of_week = 'Wednesday' THEN 4
          WHEN day_of_week = 'Thursday' THEN 5
          WHEN day_of_week = 'Friday' THEN 6
          WHEN day_of_week = 'Saturday' THEN 7
     END ASC, member_casual

```

Number of rides per month

```sql

SELECT
member_casual,
month,
rideable_type,
COUNT(*) rides_per_month
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
GROUP BY member_casual, month, rideable_type
ORDER BY CASE
          WHEN month = 'January' THEN 1
          WHEN month = 'February' THEN 2
          WHEN month = 'March' THEN 3
          WHEN month = 'April' THEN 4
          WHEN month = 'May' THEN 5
          WHEN month = 'June' THEN 6
          WHEN month = 'July' THEN 7
          WHEN month = 'August' THEN 8
          WHEN month = 'September' THEN 9
          WHEN month = 'October' THEN 10
          WHEN month = 'November' THEN 11
          WHEN month = 'December' THEN 12
     END ASC

```

Average trip duration per month

```sql

SELECT
member_casual,
month,
ROUND(AVG(duration)) avg_ride_per_month,
(
-- inner query to display shortest trip duration  
   SELECT
   MIN(duration)
   FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
  ) shortest_trip_per_month,
-- inner query to display the longest trip duration  
    (SELECT
      MAX(duration)
      FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
      )longest_trip_per_month,
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
GROUP BY member_casual, month
ORDER BY CASE
          WHEN month = 'January' THEN 1
          WHEN month = 'February' THEN 2
          WHEN month = 'March' THEN 3
          WHEN month = 'April' THEN 4
          WHEN month = 'May' THEN 5
          WHEN month = 'June' THEN 6
          WHEN month = 'July' THEN 7
          WHEN month = 'August' THEN 8
          WHEN month = 'September' THEN 9
          WHEN month = 'October' THEN 10
          WHEN month = 'November' THEN 11
          WHEN month = 'December' THEN 12
     END ASC

```

Query to diaplay the number of rides by season in relation to customer and bike type, including average trip duration for individual seasons

```sql

SELECT
member_casual,
season,
rideable_type,
COUNT(*) rides_per_season,
ROUND(AVG(duration)) avg_trip
FROM liquid-cumulus-411017.divvy_tripdata_2023.combined_tripsV02
GROUP BY member_casual, season, rideable_type

```





