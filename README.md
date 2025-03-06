# Thiru_Taxi_Assignment_IA626
## **NYC Taxi Trip Data Analysis**
### **Project Overview**

In this project, we analyze a large dataset of taxi rides in NYC. The dataset contains millions of rows, and understanding its structure, statistics, and insights is essential. The following analysis is performed:
- Understanding the **datetime range** and **total rows.**
- Extracting **field names, descriptions, and sample data.**
- Determining the **MySQL data types for storage.**
- Identifying the **geographic range (latitude/longitude).**
- Computing the **average trip distance** using the **Haversine formula.**
- Plotting a **histogram of trip distances**.
- Finding **distinct values** in each field.
- Extracting **min/max values** for other **numeric fields.**
- Analyzing the **average number of passengers per hour**.
- Creating a **reduced dataset and comparing results.**

### **Terminal Commands for Data Inspection**
Before processing the dataset, it's useful to inspect its size, structure, and sample records. The following **terminal commands** help in understanding the dataset:

1. Count the Number of Rows in the CSV File

**wc -l trip_data_6.csv**
- wc -l counts the number of lines (rows) in the file.
- Helps in understanding the dataset size.
  
2. View the Header (Column Names)

**head -n 1 trip_data_6.csv**
- head -n 1 prints the first row, which usually contains column names.
- Useful for verifying field names before processing.
  
3. View the First Few Rows of the Data

**head -n 5 trip_data_6.csv**
- head -n 5 prints the first 5 rows of the dataset.
- Helps in getting a quick preview of how data is structured.


### **1. Dataset Details**
- **Filename:** trip_data_6.csv
- **Total Rows:** 14,385,456
- **Datetime Range:** **2013-06-01** 00:00:00 to **2013-07-01** 01:14:24

### **2. Field Names & Descriptions**
<img width="738" alt="FieldNames Descriptions" src="https://github.com/user-attachments/assets/06e09036-6729-45e8-aa4c-758cc05f704e" />

### **3. Data Processing Steps**

The script processes taxi trip data from a large CSV file and performs various analyses, including:
- **Extracting trip details** such as pickup/dropoff times, locations, passenger counts, and trip distances.
- **Filtering out invalid data points** (e.g., incorrect coordinates, missing timestamps).
- **Computing summary statistics** such as min/max values for numeric fields.
- **Creating visualizations** to analyze trip distances and passenger trends.

**Data Cleaning & Validation**

The script reads a large dataset (trip_data_6.csv) and initializes variables to track:

- Number of rows processed.
- Earliest and latest trip dates.
- Geographic coordinates (latitude, longitude).
- Passenger count distribution by hour.
- Categorical fields (e.g., rate_code, store_and_fwd_flag).
- Column names are **stripped of spaces** to ensure consistency.
- **Removed invalid or extreme latitude/longitude values**
 - NYC coordinates range from **(40.5 ≤ lat ≤ 41.0, -74.3 ≤ lon ≤ -73.7).**
 - Trips with coordinates outside this range were discarded to remove invalid entries.
- **Filtered out unrealistic trip distances**
 - Some trips showed **distances exceeding 1000 km**, which is physically impossible for a NYC taxi ride.
 - Any trip with **distance > 100 km** was assumed incorrect and removed. 
- **Handled missing or incorrect data entries**
 - Rows with **missing pickup or dropoff times** were skipped.
 - Ensured all fields had the **correct data type** (e.g., passenger_count should be an integer).
   
**Date Parsing and Validation**

- The script converts pickup and dropoff timestamps to datetime format.
- It updates minimum and maximum dates encountered in the dataset.
- If a date is invalid (e.g., missing or incorrectly formatted), the **row is skipped.**
  
### 4. **Geographic Data Processing**

- The script extracts **pickup and dropoff coordinates** (longitude, latitude).
- It **validates coordinates** to ensure they are within **New York City boundaries:**
  
Latitude Range: 40.5 to 41.0
Longitude Range: -74.3 to -73.7

If coordinates are valid:
 - Trip distance is computed using the Haversine formula, which calculates the great-circle distance between two points on Earth.
 - Extreme outliers (distance > 1000 km) are filtered out.
 - Geographic range (min/max latitude and longitude) is updated dynamically.







