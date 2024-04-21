# Case-study-How-does-a-bike-share-navigate-speedy-success-
![Capture](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/a2f80b68-1dc1-4be8-bf9f-3e10b98ff532)

Author: Truong Phan

Date: April 21, 2024

## Introduction

This is my first project in the data analysis field, set in a fictional context. In this scenario, I serve as a junior data analyst working on the marketing analyst team at Cyclistic. The marketing director believes that increasing the number of annual memberships is crucial for the business’s future success. Consequently, my team aims to determine how casual riders and annual members use Cyclistic bikes differently. Our goal is to provide recommendations that will guide the marketing strategy. Guided by the Google Data Analytics Course, this project will follow the data analysis process: asking questions, preparing data, processing it using SQL in BigQuery, analyzing patterns, sharing insights through Tableau, and finally, proposing actionable strategies. 

### About Cyclistic

Cyclistic, a bike-share program launched in 2016, now boasts a fleet of 5,824 bicycles. These bikes are tracked and can be unlocked from one station and returned to any other station within the 692 stations across the Chicago network. Until now, Cyclistic’s marketing approach focused on raising general awareness and appealing to a wide range of consumers. Their pricing flexibility, including options like single-ride passes, full-day passes, and annual memberships, has successfully attracted more customers. Specifically, casual riders prefer single-ride or full-day passes. However, Cyclistic’s finance analysts have discovered that annual members are significantly more profitable. Despite the pricing flexibility, maximizing the number of annual members remains crucial for the company’s future growth.

## Body

### 1. Ask Phrase

#### 1.1. Key stakeholder

**Primary Stakeholder: Lily Moreno**

- **Role:** Director of Marketing

- **Responsibilities:** Moreno is responsible for developing campaigns and initiatives to promote the bike-share program. Her work may involve channels such as email, social media, and other marketing platforms. As your manager, she is crucial in shaping Cyclistic’s marketing strategy.

**Secondary Stakeholder: Cyclistic Marketing Analytics Team**

- **Role:** Data analysts within the marketing team

- **Responsibilities:** This team collects, analyzes, and reports data that informs Cyclistic’s marketing decisions. As a junior data analyst, I collaborate with this team to understand Cyclistic’s mission, and business goals and contribute to achieving them through data-driven insights.

**Additional Stakeholder: Cyclistic Executive Team**

- **Role:** The executive team oversees the entire organization.

- **Responsibilities:** They will ultimately decide whether to approve the recommended marketing program. Their attention to detail and strategic decision-making influence Cyclistic’s overall direction and growth.

#### 1.2. Business task statement

Analyze historical bike trip data to compare the behavior of annual members and casual riders. Identify trends that can inform the marketing team’s strategies for converting casual riders into annual members.

### 2. Prepare Phrase

#### 2.1. Information about the dataset

This case study utilized a dataset from a bike-sharing company. The data was publicly available and could be used to explore how different customer types utilize Cyclistic bikes. The dataset consisted of 12 .csv files in long format, containing information on bicycle trips from January 2023 to December 2023. 

#### 2.2. Data accessibility

The data has been made available by Motivate International Inc. The dataset’s license grants a non-exclusive, royalty-free, limited, and perpetual license to access, reproduce, analyze, copy, modify, distribute, and use the data for any lawful purpose. Therefore, I used this data as source material in my project report for non-commercial purposes 

#### 2.3. Is this data ROCCC ?

**Reliable**:  The dataset appeared to be sourced from official bike-share systems, which suggested reliability. However, to fully assess reliability, I would need additional information about the data collection process, quality control, and any potential biases.

**Original**: The data was publicly available and could be located at the provided link. It was an original dataset.

**Comprehensive**: The dataset covered various variables and dimensions, such as rideable type, trip durations,  station name, member or casual, and other relevant details. This level of detail made it comprehensive for bike-share analysis.

**Current**: The dataset was current as it was collected in 2023 which aligns with the specified timeframe.

**Cited**: The link to the data didn’t include citations, so it definitely couldn't be cited.

#### 2.1. Limitations

Due to data privacy concerns, access to riders’ personally identifiable information is restricted. Consequently, it was impossible to determine whether casual riders resided within the Cyclistic service area or if they had purchased multiple single passes. Additionally, the absence of demographic information in the data could introduce sampling bias.

### 3. Process Phase

In the process phase, I leveraged SQL to import, clean, and transform a large dataset containing millions of records (5719877). These critical activities were executed within Google BigQuery, a fully managed enterprise data warehouse provided by Google Cloud. BigQuery offered powerful features for efficient data management and analysis.

#### 3.1. Import data  

I uploaded .csv files into tables with name conventions from Cyclistic_Trip_January to Cyclistic_Trip_December. In this step, I also separated some files into two parts because the capacity exceeds BiqQuery's upload limit of 100mb. 

#### 3.2. Merge Data

UNION ALL operator was used to merge tables into new ones named Cyclistic_Trip_2023, This operator could help keep the original records, even duplicated records. 

```
CREATE TABLE
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023` AS
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_January`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_February`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_March`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_April`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_May_part_1`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_May_part_2`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_June_part_1`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_June_part_2`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_July_part_1`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_July_part_2`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_August_part_1`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_August_part_2`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_September_part_1`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_September_part_2`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_October_part_1`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_October_part_2`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_November`
 UNION ALL
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_December`
```

#### 3.3. Checking data structure and data type

Reviewing the schema of the ‘Cyclistic_Trip_2023’ table, it could be seen that fields such as STRING for text-based data and TIMESTAMP for date/time data are correctly assigned. FLOAT was used for latitude and longitude coordinates, which were also appropriately formatted.

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/1e5657a6-a8bf-42c9-b9e7-b4236b469bc7)

- ride_id: This is a unique identifier for each trip, helping to distinguish between different trips.

- rideable_type: The type of bicycle used for the trip, such as a standard bike, electric bike, etc.

- started_at and ended_at: The start and end times of the trip.

- start_station_name and end_station_name: The names of the starting and ending stations for the trip.

- start_lat and start_lng, end_lat, and end_lng: The latitude and longitude coordinates of the starting and ending points of the trip.

- member_casual: Classification of the user as a member or a casual (non-member) rider.

#### 3.4. Checking duplicates

I began cleaning data with the DISTINCT operator to check duplicates. This operator helped display a subset of data that only shows unique records.

```
SELECT
 COUNT(DISTINCT ride_id) AS total_distinct_rows
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023`
```
![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/e4b5c3d3-9408-46ae-ad3d-83161b6accf4)

After running the query, the result showed the total records of 5719877 the same as the original. So I state that there is no duplicate in the data.

#### 3.5. Handle Missing Values

I previewed the data frame and found that there are missing values in the start_station_name, start_station_id, end_station_name, and end_station_id. So, I used IS NULL to check how many records contain missing values in these columns.

```
SELECT
 COUNT(*) AS total_nulls
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023`
WHERE
 start_station_name IS NULL OR start_station_id IS NULL OR end_station_id IS NULL OR end_station_name IS NULL
```
![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/754e513d-4f28-4b78-882b-29631769f32b)

There are 1388054 records containing NULL values in data which capture 24% Cyclistic_Trip_2023. I decided to remove these records to ensure the analysis process was not affected. IS NOT NULL will be used to remove NULL records and the result will be saved in a new table named ”Cyclistic_Trip_2023_Clean”

```
CREATE TABLE
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_Clean` AS
 SELECT *
 FROM
  `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023`
 WHERE
  (start_station_id IS NOT NULL AND start_station_name IS NOT NULL) AND (end_station_id IS NOT NULL AND end_station_name IS NOT NULL)
```

#### 3.6. Adding New Columns and Removing Unnecessary Columns

In order to gain both an overview and detailed insights into the patterns of bike-sharing service users, I decided to create new columns for our dataset. Firstly, I utilized the EXTRACT function to extract detailed time information from the started_at column. Specifically, I extracted the hour (hour), day of the week (day_of_week), and month (month) of each bike ride's start time. Additionally, I used the TIMESTAMP_DIFF function to compute the duration of each bike ride based on its start and end times, with the result stored in the duration_mins column. Upon careful consideration, I observed that the longitude and latitude columns did not provide useful or correctly positioned information when using Google Maps. Therefore, I opted to remove these two columns from the dataset. Eliminating unnecessary columns helped reduce the size of the dataset and focus on more pertinent information for analysis.
Below is the SQL code illustrating these steps:

```
CREATE TABLE
`cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_new` AS
 SELECT
    ride_id,
    rideable_type,
    EXTRACT(HOUR FROM started_at) AS hour,
    EXTRACT(DAYOFWEEK FROM started_at) AS day_of_week,
    EXTRACT(MONTH FROM started_at) AS month,
    TIMESTAMP_DIFF(ended_at, started_at, MINUTE) AS duration_mins,
    start_station_id,
    start_station_name,
    end_station_id,
    end_station_name,
    member_casual
  FROM
   `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_Clean`
```

#### 3.7. Solving negative and too-large values

When double-checking the data, I found some unusual records. The duration_mins column of these records had the containing negative values or very large values. Then, I used COUNTIF() to see how many records in total contain unusual durations.

```
SELECT
 COUNTIF(duration_mins <= 0) AS Negative,
 COUNTIF(duration_mins >= 1440) AS Too_large
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_new`
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/fcfef45c-7348-4ee7-993d-2338b3daaa8d)

There were a total of 87651 unusual records. This would impact the duration analysis if I keep these records. So I continued to remove records. At the same time, I also used CASE to convert the values 1 to 7 in the weekday column to Sunday to Saturday. This makes it easier to see during analysis and visualization. The results will be saved in a new table named Cyclistic_trip_2023_final.

```
CREATE TABLE
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final` AS
 SELECT
  ride_id,
  rideable_type,
  hour,
  CASE day_of_week
        WHEN 1 THEN 'Sunday'
        WHEN 2 THEN 'Monday'
        WHEN 3 THEN 'Tuesday'
        WHEN 4 THEN 'Wednesday'
        WHEN 5 THEN 'Thursday'
        WHEN 6 THEN 'Friday'
        WHEN 7 THEN 'Saturday'
 END AS day_of_week,
   month,
 duration_mins,
 start_station_id,
 start_station_name,
 end_station_id,
 end_station_name,
 member_casual
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_new`
WHERE
 duration_mins > 0 AND duration_mins < 1440
```

### 4. Analyze Phrase

#### 4.1.Total trips

First of all, I compared the total number of trips taken by members and casual customers on a monthly, weekly, and hourly basis. I examined which group contributed more to their preferred trip volume and rideable types.

```
SELECT
 member_casual,
 COUNT (*) AS total_trips,
 COUNTIF(rideable_type = "docked_bike") AS docked_bike_trips,
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
GROUP BY
 member_casual
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/fecbc548-420d-4e14-bc3e-4aec7fa2aca6)

In total, members were the driving force behind total trips (2,738,867 trips), indicating their strong engagement with Cyclistic services. Both casual and member customers favored classic bikes. Again, members led the way with 950,116 electric bike trips, compared to casuals’ 569,179. Interestingly, casual customers also used docked bikes, while members didn’t utilize them.

##### 4.1.1. Monthly Trips

**Member**

```
SELECT
 month,
 COUNT (*) AS number_trips, 
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "member"
GROUP BY
 month
ORDER BY
 number_trips DESC
```
![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/d3ff58a9-61ed-4a17-9823-2d950159c962)

The highest number of member trips occurred during the warmer months, with July and August being the peak months. As the weather cooled down, the number of trips decreased significantly. Classic bikes were the top choice among members.

**Casuals**

```
SELECT
 month,
 COUNT (*) AS number_trips,
 COUNTIF(rideable_type = "docked_bike") AS docked_bike_trips,
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "casual"
GROUP BY
 month
ORDER BY
 number_trips DESC
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/be3ab66d-3438-4a31-966c-1a5c7f6bf670)

Like members, casuals tended to take more trips during the warmer months, while trip numbers decreased in the cooler months. Among casual riders, classic bikes were the preferred choice, followed by electric bikes. Docked bikes are the least used and even there are no trips from September to December. 

##### 4.1.2. Weekly trips

**Member**

```
SELECT
 day_of_week,
 COUNT (*) AS number_trips,
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "member"
GROUP BY
 day_of_week
ORDER BY
 number_trips DESC
```
![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/44a96eec-f0f5-4549-9822-89e2af4b8c67)

Cyclistic members took the most trips on Tuesday, Wednesday, and Thursday, with fewer trips as the weekend approached. Sunday had the lowest member activity. Classic bikes were the most popular choice throughout the week, followed by electric bikes.

**Casuals**

```
SELECT
 day_of_week,
 COUNT (*) AS number_trips,
 COUNTIF(rideable_type = "docked_bike") AS docked_bike_trips,
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "casual"
GROUP BY
 day_of_week
ORDER BY
 number_trips DESC
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/3056e1c0-fa95-4986-8b73-4435511dfbcb)

In contrast to members, casuals were most active on weekend days. The number of trips decreased progressively on weekdays. Electric bike trips were particularly popular among casuals.

##### 4.1.3. Hourly trips

**Member**

```
SELECT
 hour,
 COUNT(*) AS total_trips,
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "member"
GROUP BY
 hour
ORDER BY
 total_trips DESC
```
![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/1571d090-e339-4eb9-92ae-7be8d6e0ddd5)

The data shows that members were active throughout the day, with the evening being the busiest period when a large number of trips took place. Trip numbers decreased significantly during the night. Notably, classic bikes were used for more trips compared to electric bikes.

**Casuals**

```
SELECT
 hour,
 COUNT(*) AS total_trips,
 COUNTIF(rideable_type = "docked_bike") AS docked_bike_trips,
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "casual"
GROUP BY
 hour
ORDER BY
 total_trips DESC
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/4a9ddb76-812f-4eb2-ade3-a9b257c9e83a)

Contrary to members, the majority of casual customers tended to start their trips in the afternoon and evening. Among the available options, classic bikes were the most preferred choice, followed by electric bikes and docked bikes.

#### 4.2. Duration of bicycle use

Next, I investigated the minimum, maximum, and average usage duration (in minutes) for both members and casual customers. 

**Member**

```
SELECT
 MIN(duration_mins) AS Min,
 MAX(duration_mins) AS MAX,
 AVG(duration_mins) AS AVG
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "member"
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/16f8b1c9-6b3f-4934-88f2-c9adeee31e87)

Member customers had a wide range of usage durations, with the shortest recorded at 1 minute and the longest at 1,439 minutes. This indicated that some members may take very brief trips or perhaps test the bikes briefly. While some others relied heavily on the service for extended periods, possibly for leisurely rides, commuting, or longer travel. On average, customers used the service for approximately 11.88 minutes, suggesting most used it for short journeys.

**Casuals**

```
SELECT
 MIN(duration_mins) AS Min,
 MAX(duration_mins) AS MAX,
 AVG(duration_mins) AS AVG
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "casual"
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/046a642e-20b0-4b8a-8038-bd014bfa0506)

Similar to member customers, casual bicycle trips had a minimum duration of 1 minute. The maximum duration for casual bicycle trips was slightly lower than that for members. However, the average duration for casual bicycle trips was nearly twice as many as members. This suggested that most casual riders tended to take medium-length journeys.

**Duration by rideable types**

Additionally, I broke down the usage duration by rideable types.

**Member**

```
SELECT
 rideable_type,
 MIN(duration_mins) AS Min,
 MAX(duration_mins) AS MAX,
 AVG(duration_mins) AS AVG
 FROM `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "member"
GROUP BY
 rideable_type
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/62be2d53-f212-4137-b52b-6fbcc4cb3cfb)

Classic and electric bikes had the same minimum usage duration of 1 minute. About maximum, electric bikes generally had a shorter usage duration. The average of the two rideable types was nearly equal (12.68 vs 10.37 minutes) indicating members used these types for short trips. 

**Casuals**

```
SELECT
 rideable_type,
 MIN(duration_mins) AS Min,
 MAX(duration_mins) AS MAX,
 AVG(duration_mins) AS AVG
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "casual"
GROUP BY
 rideable_type
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/2afc5390-c7b2-48f8-9f85-7b854eeb9885)

The minimum ride duration for all three types of bikes was 1 minute. Among them, docked bikes had the highest maximum duration. Electric bikes were commonly used for short trips, averaging around 14.5 minutes, while classic bikes served medium trips with approximately 25.5 minutes. Docked bikes were preferred for longer journeys, with an average usage time of 52 minutes.

#### 4.3. Top start stations

I identified the top 5 start stations based on total trips. Furthermore, I analyzed these stations by rideable types to understand preferences.

**Member**

```
SELECT
 start_station_name,
 COUNT(*) AS total_trips,
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "member"
GROUP BY
 start_station_name
ORDER BY
 total_trips DESC
LIMIT 5
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/83ead9af-2bce-46a7-a1ce-1e876efa75d5)

The starting stations for members were typically situated in the northwest area of Chicago city. Among them, Kingsbury St & Kinzie St, Clinton St & Washington Blvd, and Clark St & Elm St emerged as the top destinations, consistently drawing a substantial number of riders. Classic bicycles were the most popular choice at all these stations.

**Casuals**

```
SELECT
 start_station_name,
 COUNT(*) AS total_trips,
 COUNTIF(rideable_type = "docked_bike") AS docked_bike_trips,
 COUNTIF(rideable_type = "classic_bike") AS classic_bike_trips,
 COUNTIF(rideable_type = "electric_bike") AS electric_bike_trips,
FROM
 `cyclistic-417415.Cyclistic_history_trips_data.Cyclistic_Trip_2023_final`
WHERE
 member_casual = "casual"
GROUP BY
 start_station_name
ORDER BY
 total_trips DESC
LIMIT 5
```

![image](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/ec684c7b-896c-4f52-b93f-e3b9806bfc60)

Unlike members, casual customers tended to favor start stations in the northeast of Chicago city. Streeter Dr & Grand Ave, DuSable Lake Shore Dr & Monroe St, and Michigan Ave & Oak St emerged as the top choices for most riders. Classic bikes were the most preferred ride option across all these stations.

### 5. Share Phrase

In the Share Phase of our data analysis process, I developed a comprehensive dashboard using Tableau Public to present key insights from our examination of Cyclistic trip data for the year 2023. This visual analysis focused specifically on comparing the behaviors and patterns of Cyclistic's members and casuals across various metrics, including total trips taken, usage duration, and popular starting stations.

#### 5.1. Visualizations
**Members**

![Tableau de bord 1 (2)](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/ee842f30-9afb-4fcc-b503-7a54c8d78c59)

**Casuals**

![Tableau de bord 1 (3)](https://github.com/Truong127/Case-study-How-does-a-bike-share-navigate-speedy-success-/assets/160266278/0f7085fa-0204-4263-b3ce-f7f51b23fe35)

Viewers can also access the dashboard here: [https://public.tableau.com/views/CyclisticTrips2023/Tableaudebord1?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link]

#### 5.2. Key findings

- Members took more trips than casual customers.
  
- Classic bikes were the preferred choice for both members and casual customers, followed by electric bikes.
  
- Casual customers used docked bikes, whereas members did not.
  
- Casual riders typically opt for medium-length trips, while members prefer shorter ones.
  
- Members favored classic and electric bikes for short trips, while casual customers used docked bikes for long trips, classic bikes for medium trips, and electric bikes for short trips.
  
- Member start stations were mainly located in the northwest of Chicago, while casual riders tended to start in the northeast.
  
- Trip volumes for both members and casuals increased during warmer months and decreased in cooler ones.
  
- Members were more active on weekdays, whereas casual customers tended to ride more on weekends.
  
- Members preferred riding throughout the day, from morning to evening, while casual riders primarily took trips in the afternoon and evening.

### 6. Act Phrase

**Top recommendations**

- Event Series in the Northeast: Launch a series of engaging community events in parks and popular public spaces in the northeast of Chicago. These events are designed to highlight the advantages of being a member, including convenient access and exclusive benefits such as guaranteed bike availability, reward points, and the opportunity for non-members to try the services at no cost.

- Warm Weather Campaigns: Introduce a ‘Summer Ride Pass’ that offers unlimited rides during the warmer months at a flat rate, with the option to convert to a full membership at the end of the season.
  
- Weekend Family Packages: Offer discounted group rates for families or friends to enjoy weekend rides together, potentially including guided tour options to explore new areas.
  
- Off-Peak Incentives: Implement a dynamic pricing model where rides are cheaper during off-peak hours, encouraging usage throughout the day and reducing congestion during peak times.
  
- Long Trip Switch Promotion: Encourage casual riders to try classic or electric bikes for their longer trips with a ‘Switch & Save’ campaign, offering a significant discount on the first few rides when switching from docked bikes.

## Conclusion

This project presented both a significant challenge and a valuable learning opportunity. Throughout its course, I knew how to carry out six phases of data analysis. Utilizing tools such as SQL in BigQuery, and Tableau, I was able to use data to address the problem. My analysis culminated in recommendations that could inform the company's marketing strategy effectively.

Despite these successes, the project was not without its limitations. Notably, there was a considerable loss of data during the processing phase, and not all available data fields were leveraged. Certain aspects of the presentation also lacked clarity. Additionally, the project could have benefited from more robust data modeling, hypothesis testing, and so on.

In conclusion, this experience has reinforced my belief in the critical importance of data analysis skills. In today's data-driven world, proficiency in data analysis is essential for enhancing business operations and driving strategic decisions.
