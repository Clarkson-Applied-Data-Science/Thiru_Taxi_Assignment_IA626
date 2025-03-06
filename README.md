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
  
### **1. Dataset Details**
- **Filename:** trip_data_6.csv
- **Total Rows:** 14,385,456
- **Datetime Range:** 2013-06-01 00:00:00 to 2013-07-01 01:14:24

### **2. Field Names & Descriptions**
<img width="738" alt="Screenshot 2025-03-05 at 10 38 08 PM" src="https://github.com/user-attachments/assets/ca7f3d75-c204-4375-a3e7-62740f09814e" />

### **3. Data Processing Steps**
**Data Cleaning & Validation**
-- Removed invalid or extreme latitude/longitude values
- NYC coordinates range from (40.5 ≤ lat ≤ 41.0, -74.3 ≤ lon ≤ -73.7).
- Trips with coordinates outside this range were discarded to remove invalid entries.
-- Filtered out unrealistic trip distances
•	Some trips showed distances exceeding 1000 km, which is physically impossible for a NYC taxi ride.
•	Any trip with distance > 100 km was assumed incorrect and removed.
✔ Handled missing or incorrect data entries
•	Rows with missing pickup or dropoff times were skipped.
•	Ensured all fields had the correct data type (e.g., passenger_count should be an integer).





