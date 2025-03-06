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

### **2. Field Names & Descriptions | MySQL data types / len**
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
- It updates the minimum and maximum dates encountered in the dataset.
- If a date is invalid (e.g., missing or incorrectly formatted), the **row is skipped.**

# Output 
1. **DateTime Range:** 2013-06-01 00:00:00 to 2013-07-01 01:14:24
2. **Total Rows:** 14385456
3. **Field Names:** ['medallion', 'hack_license', 'vendor_id', 'rate_code', 'store_and_fwd_flag', 'pickup_datetime', 'dropoff_datetime', 'passenger_count', 'trip_time_in_secs', 'trip_distance', 'pickup_longitude', 'pickup_latitude', 'dropoff_longitude', 'dropoff_latitude']
**Sample Data:** [['D1C79CF706C80D3A1DC7FBCA6CD56E43', 'DAC7742E8F00034774098DBC6B4FF2B7', 'CMT', '1', 'N', '2013-06-03 00:02:12', '2013-06-03 00:10:07', '1', '474', '1.30', '-73.981583', '40.773529', '-73.981827', '40.782124'], ['3567E8B49FEBFCBB587F1864D723D5C8', '430B8022563CDE1D51D44786DFD8D6CB', 'CMT', '1', 'N', '2013-06-03 00:03:03', '2013-06-03 00:19:27', '1', '982', '4.90', '-73.999565', '40.728367', '-73.952927', '40.729546'], ['4220E1995D36A40DF34664AD33ED13F6', '48A1C9C9300AFC7BDBB718CE308EE45A', 'CMT', '2', 'N', '2013-06-03 00:01:30', '2013-06-03 00:28:11', '1', '1745', '17.70', '-73.788445', '40.641151', '-73.985451', '40.744194'], ['440900089FF528A873424DED689C77A3', 'E6A63B40E565A8A03AF32E0B138F5EB1', 'CMT', '1', 'N', '2013-06-03 00:04:14', '2013-06-03 00:27:50', '1', '1415', '12.10', '-73.862816', '40.768875', '-74.008797', '40.738842'], ['16129167D9E7B0846DBA3D04B78E1B8D', '227A03FC03CF429DFC9EAFF0AE8BA579', 'CMT', '1', 'N', '2013-06-03 00:04:53', '2013-06-03 00:10:46', '1', '353', '1.10', '-73.964905', '40.806881', '-73.962349', '40.794987']]
4. **Geographic Range:**
  Pickup Longitude: -74.3 to -73.7
  Pickup Latitude: 40.5 to 41.0
  Dropoff Longitude: -74.3 to -73.7
  Dropoff Latitude: 40.5 to 41.0
5. **Average Trip Distance:** 3.44 km
6. **Distinct Values per Field:**
rate_code: 11 distinct values
store_and_fwd_flag: 3 distinct values
7. **Numeric Field Min/Max Values:**
rate_code: Min=0.0, Max=210.0
passenger_count: Min=0.0, Max=208.0
trip_time_in_secs: Min=0.0, Max=10800.0
trip_distance: Min=0.0, Max=100.0

### 4. **Geographic Data Processing**

- The script extracts **pickup and dropoff coordinates** (longitude, latitude).
- It **validates coordinates** to ensure they are within **New York City boundaries:**
  
Latitude Range: 40.5 to 41.0

Longitude Range: -74.3 to -73.7

If coordinates are valid:
 - Trip distance is computed using the Haversine formula, which calculates the great-circle distance between two points on Earth.
 - Extreme outliers (distance > 1000 km) are filtered out.
 - Geographic range (min/max latitude and longitude) is updated dynamically.

<img width="1344" alt="GeographicRange" src="https://github.com/user-attachments/assets/0e61feab-8ae1-4077-a04a-43bc3a23676d" />


### 5. Trip Distance Calculation (Haversine Formula)
-	Used the Haversine formula to calculate the actual distance between pickup and drop-off locations.
-	Accounts for the curvature of the Earth for accurate distance measurement.


### **6. Tracking Distinct Categorical Values**
- The script maintains a set of distinct values for categorical fields (rate_code, store_and_fwd_flag).
- This helps in understanding how many different categories exist in the dataset.

### **7. Hourly Passenger Count Analysis**
- The script groups passenger counts by hour (based on pickup time).
- This allows for trend analysis to see when the highest number of passengers travel.

### **8. Numeric Field Statistics**

The script updates min/max values for numeric fields:
- rate_code
- passenger_count
- trip_time_in_secs
- trip_distance
  
This helps in understanding the range of values in the dataset.

### **9. Generating a Reduced Dataset**
- Since the original dataset is very large, a reduced version (reduced_trip_data.csv) is created.
- The script selects every 1000th row to create a smaller, more manageable dataset.
- This reduced dataset is later used for comparison with the full dataset.

### **10. Data Visualization**

The script generates three key visualizations:

**Histogram of Trip Distances**

- X-axis: Trip distance (km)
- Y-axis: Frequency (log scale)
- Helps identify common trip distances and detect outliers.

![Hist_Trip_Distance_output](https://github.com/user-attachments/assets/c179ba48-42be-4625-beda-c50551c6b78a)


**Hourly Passenger Count (Full Data)**
- X-axis: Hour of the day
- Y-axis: Average number of passengers
- Helps determine peak travel hours.

![FullData_Chart_output](https://github.com/user-attachments/assets/e79fb418-3b02-4cb1-804b-c124d2585258)


**Hourly Passenger Count (Subset)**
-	X-axis: Hour of the day
-	Y-axis: Average number of passengers
-	Helps determine peak travel hours from the subset.

![Subset_Chart_output](https://github.com/user-attachments/assets/aec70093-f990-4270-8df9-c734e9070371)


**Comparison of Full vs. Subset**
-	Line charts compare hourly passenger trends between the full dataset and the reduced dataset.
-	Helps verify whether the reduced dataset maintains similar trends as the full dataset.

![Comparison_Chart_output](https://github.com/user-attachments/assets/4af277e5-aaeb-4637-a543-e6cf8badb601)

# Code

```python
import csv
import datetime
import matplotlib.pyplot as plt
from collections import defaultdict
from math import radians, sin, cos, sqrt, atan2

# File Path
filename = "trip_data_6.csv"

# Initialize variables
num_rows = 0
min_date, max_date = None, None
field_names = []
sample_data = []
trip_distances = []
hourly_passenger_count = defaultdict(list)
distinct_values = defaultdict(set)

# NYC latitude ranges from ~40.5 to 41
# NYC longitude ranges from ~-74.3 to -73.7
numeric_fields = {
    'pickup_longitude': {'min': -74.3, 'max': -73.7},
    'pickup_latitude': {'min': 40.5, 'max': 41.0},
    'dropoff_longitude': {'min': -74.3, 'max': -73.7},
    'dropoff_latitude': {'min': 40.5, 'max': 41.0},
}
numeric_fields1 = {
    'rate_code': {'min': float('inf'), 'max': float('-inf')},
    'passenger_count': {'min': float('inf'), 'max': float('-inf')},
    'trip_time_in_secs': {'min': float('inf'), 'max': float('-inf')},
    'trip_distance': {'min': float('inf'), 'max': float('-inf')}
}


# Define valid coordinate range
VALID_LAT_RANGE = (40.5, 41.0)
VALID_LON_RANGE = (-74.3, -73.7)

# Define categorical fields (to track distinct values efficiently)
categorical_fields = {'rate_code', 'store_and_fwd_flag'}

# Function to compute Haversine distance
def haversine(coord1, coord2):
    R = 6371.0  # Earth radius in km
    lat1, lon1 = map(radians, coord1)
    lat2, lon2 = map(radians, coord2)
    dlat = lat2 - lat1
    dlon = lon2 - lon1
    a = sin(dlat / 2)**2 + cos(lat1) * cos(lat2) * sin(dlon / 2)**2
    c = 2 * atan2(sqrt(a), sqrt(1 - a))
    return R * c
# Read the CSV file
with open(filename, 'r') as f:
    reader = csv.reader(f)
    field_names = [field.strip() for field in next(reader)]  # Remove spaces from column names

    for i, row in enumerate(reader):
        num_rows += 1
        
        # Capture sample data
        if i < 5:
            sample_data.append(row)
        
        # Parse dates
        try:
            pickup_datetime = datetime.datetime.strptime(row[5], "%Y-%m-%d %H:%M:%S")
            dropoff_datetime = datetime.datetime.strptime(row[6], "%Y-%m-%d %H:%M:%S")
        except (ValueError, IndexError):
            continue
        
        if min_date is None or pickup_datetime < min_date:
            min_date = pickup_datetime
        if max_date is None or dropoff_datetime > max_date:
            max_date = dropoff_datetime
        
        # Parse geographic coordinates
        try:
            pickup_lon, pickup_lat = float(row[10]), float(row[11])
            dropoff_lon, dropoff_lat = float(row[12]), float(row[13])
            
            # Validate coordinates
            if (VALID_LAT_RANGE[0] <= pickup_lat <= VALID_LAT_RANGE[1] and 
                VALID_LON_RANGE[0] <= pickup_lon <= VALID_LON_RANGE[1] and 
                VALID_LAT_RANGE[0] <= dropoff_lat <= VALID_LAT_RANGE[1] and 
                VALID_LON_RANGE[0] <= dropoff_lon <= VALID_LON_RANGE[1]):
                
                # Calculate Haversine distance
                distance = haversine((pickup_lat, pickup_lon), (dropoff_lat, dropoff_lon))
                if distance < 1000:  # Filtering out extreme outliers
                    trip_distances.append(distance)
                
                # Update geographic range
                numeric_fields['pickup_longitude']['min'] = min(numeric_fields['pickup_longitude']['min'], pickup_lon)
                numeric_fields['pickup_longitude']['max'] = max(numeric_fields['pickup_longitude']['max'], pickup_lon)
                numeric_fields['pickup_latitude']['min'] = min(numeric_fields['pickup_latitude']['min'], pickup_lat)
                numeric_fields['pickup_latitude']['max'] = max(numeric_fields['pickup_latitude']['max'], pickup_lat)
                numeric_fields['dropoff_longitude']['min'] = min(numeric_fields['dropoff_longitude']['min'], dropoff_lon)
                numeric_fields['dropoff_longitude']['max'] = max(numeric_fields['dropoff_longitude']['max'], dropoff_lon)
                numeric_fields['dropoff_latitude']['min'] = min(numeric_fields['dropoff_latitude']['min'], dropoff_lat)
                numeric_fields['dropoff_latitude']['max'] = max(numeric_fields['dropoff_latitude']['max'], dropoff_lat)
            else:
                print(f"Skipping invalid coordinates: ({pickup_lat}, {pickup_lon}) -> ({dropoff_lat}, {dropoff_lon})")

        except (ValueError, IndexError):
            continue
        
        # Track distinct categorical values
        for index, value in enumerate(row):
            field = field_names[index]
            if field in categorical_fields:
                distinct_values[field].add(value)
                
        # Collect hourly passenger count
        try:
            hour = pickup_datetime.hour
            passenger_count = int(row[7])
            hourly_passenger_count[hour].append(passenger_count)
        except (ValueError, IndexError):
            continue
        
        # Update numeric fields (only for valid numeric fields)
        for index, value in enumerate(row):
            try:
                num_value = float(value)
                if field_names[index] in numeric_fields1:
                    field = field_names[index]
                    numeric_fields1[field]['min'] = min(numeric_fields1[field]['min'], num_value)
                    numeric_fields1[field]['max'] = max(numeric_fields1[field]['max'], num_value)
            except ValueError:
                pass

# Compute final statistics
average_trip_distance = sum(trip_distances) / len(trip_distances) if trip_distances else 0

# Plot histogram of trip distances
plt.figure(figsize=(8, 6))
plt.hist(trip_distances, bins=50, edgecolor='black', log=True)
plt.xlabel('Trip Distance (km)')
plt.ylabel('Frequency')
plt.title('Histogram of Trip Distances')
plt.show()

# Compute hourly passenger average
hourly_avg_passengers = {hour: sum(counts) / len(counts) for hour, counts in hourly_passenger_count.items() if counts}

# Plot hourly passenger count
plt.figure(figsize=(10, 5))
plt.bar(hourly_avg_passengers.keys(), hourly_avg_passengers.values(), color='skyblue')
plt.xlabel('Hour of the Day')
plt.ylabel('Average Passengers')
plt.title('Average Number of Passengers Per Hour')
plt.xticks(range(24))
plt.ylim(1, 2.5)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()

# Print results
print(f"DateTime Range: {min_date} to {max_date}")
print(f"Total Rows: {num_rows}")
print(f"Field Names: {field_names}")
print(f"Sample Data: {sample_data}")
print(f"Geographic Range:")
print(f"  Pickup Longitude: {numeric_fields['pickup_longitude']['min']} to {numeric_fields['pickup_longitude']['max']}")
print(f"  Pickup Latitude: {numeric_fields['pickup_latitude']['min']} to {numeric_fields['pickup_latitude']['max']}")
print(f"  Dropoff Longitude: {numeric_fields['dropoff_longitude']['min']} to {numeric_fields['dropoff_longitude']['max']}")
print(f"  Dropoff Latitude: {numeric_fields['dropoff_latitude']['min']} to {numeric_fields['dropoff_latitude']['max']}")
print(f"Average Trip Distance: {average_trip_distance:.2f} km")
print(f"Distinct Values per Field:")
for field, values in distinct_values.items():
    print(f"{field}: {len(values)} distinct values")
print(f"Numeric Field Min/Max Values:")
for field, stats in numeric_fields1.items():
    print(f"{field}: Min={stats['min']}, Max={stats['max']}")

# Create a new CSV file with 1 out of every 1000 rows
reduced_filename = "reduced_trip_data.csv"
with open(filename, 'r') as f, open(reduced_filename, 'w', newline='') as f2:
    reader = csv.reader(f)
    writer = csv.writer(f2)
    writer.writerow(next(reader))  # Write header
    
    for i, row in enumerate(reader):
        if i % 1000 == 0:
            writer.writerow(row)
print("Reduced dataset created: reduced_trip_data.csv")

import csv
import datetime
import matplotlib.pyplot as plt
from collections import defaultdict

# File Path for reduced dataset
filename_reduced = "reduced_trip_data.csv"

# Initialize variables
hourly_passenger_count_reduced = defaultdict(list)

# Read the reduced CSV file
with open(filename_reduced, 'r') as f:
    reader = csv.reader(f)
    field_names = [field.strip() for field in next(reader)]  # Remove spaces from column names

    for i, row in enumerate(reader):
        # Parse dates and passenger count
        try:
            pickup_datetime = datetime.datetime.strptime(row[5], "%Y-%m-%d %H:%M:%S")
            passenger_count = int(row[7])
        except (ValueError, IndexError):
            continue
        
        # Collect hourly passenger count for reduced data
        try:
            hour = pickup_datetime.hour
            hourly_passenger_count_reduced[hour].append(passenger_count)
        except (ValueError, IndexError):
            continue

# Compute hourly passenger average for reduced dataset
hourly_avg_passengers_reduced = {hour: sum(counts) / len(counts) for hour, counts in hourly_passenger_count_reduced.items() if counts}

# Plot hourly passenger count for reduced dataset
plt.figure(figsize=(10, 5))
plt.bar(hourly_avg_passengers_reduced.keys(), hourly_avg_passengers_reduced.values(), color='blue')
plt.xlabel('Hour of the Day')
plt.ylabel('Average Passengers')
plt.title('Average Number of Passengers Per Hour (Reduced Data)')
plt.xticks(range(24))
plt.ylim(1, 2.5)
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()

import csv
import datetime
import matplotlib.pyplot as plt
from collections import defaultdict

# File Paths for both datasets
filename_full = "trip_data_6.csv"
filename_reduced = "reduced_trip_data.csv"

# Initialize variables for both datasets
hourly_passenger_count_full = defaultdict(list)
hourly_passenger_count_reduced = defaultdict(list)

# Function to process the CSV files
def process_data(filename, hourly_passenger_count):
    with open(filename, 'r') as f:
        reader = csv.reader(f)
        field_names = [field.strip() for field in next(reader)]  # Remove spaces from column names

        for row in reader:
            try:
                pickup_datetime = datetime.datetime.strptime(row[5], "%Y-%m-%d %H:%M:%S")
                passenger_count = int(row[7])
            except (ValueError, IndexError):
                continue
            
            # Collect hourly passenger count for each dataset
            try:
                hour = pickup_datetime.hour
                hourly_passenger_count[hour].append(passenger_count)
            except (ValueError, IndexError):
                continue

# Process the full and reduced datasets
process_data(filename_full, hourly_passenger_count_full)
process_data(filename_reduced, hourly_passenger_count_reduced)

# Compute hourly passenger averages for both datasets
hourly_avg_passengers_full = {hour: sum(counts) / len(counts) for hour, counts in hourly_passenger_count_full.items() if counts}
hourly_avg_passengers_reduced = {hour: sum(counts) / len(counts) for hour, counts in hourly_passenger_count_reduced.items() if counts}

# Plot comparison of hourly passenger counts using line charts
plt.figure(figsize=(14, 6))

# Plot for full dataset
plt.subplot(1, 2, 1)  # (rows, columns, index)
plt.plot(hourly_avg_passengers_full.keys(), hourly_avg_passengers_full.values(), color='skyblue', marker='o', linestyle='-', label='Full Data')
plt.xlabel('Hour of the Day')
plt.ylabel('Average Passengers')
plt.title('Full Data - Average Passengers Per Hour')
plt.xticks(range(24))
plt.ylim(1, 2.5)
plt.grid(True, axis='y', linestyle='--', alpha=0.7)
plt.legend()

# Plot for reduced dataset
plt.subplot(1, 2, 2)
plt.plot(hourly_avg_passengers_reduced.keys(), hourly_avg_passengers_reduced.values(), color='lightcoral', marker='o', linestyle='-', label='Reduced Data')
plt.xlabel('Hour of the Day')
plt.ylabel('Average Passengers')
plt.title('Reduced Data - Average Passengers Per Hour')
plt.xticks(range(24))
plt.ylim(1, 2.5)
plt.grid(True, axis='y', linestyle='--', alpha=0.7)
plt.legend()

# Show the plots
plt.tight_layout()
plt.show()















