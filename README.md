# AtliQ Hotel chain Booking Analysis

AtliQ is a fictional hotel chain operating across four cities in India. Despite being in the industry for many years, the company has been losing market share to competitors. This project digs into their booking data to find what is working and what is not.

## What This Project Covers

The analysis is done in a Jupyter Notebook using Python, Pandas and Matplotlib. It follows a structured approach starting from raw data, cleaning it up, and then pulling out insights that actually matter to the business.

Four main stages:
- Data Import and Exploration
- Data Cleaning
- Data Transformation
- Insights Generation

## Dataset

| File | Rows | Description |
|------|------|-------------|
| dim_hotels.csv | 25 | Hotel names, category, city |
| dim_rooms.csv | 4 | Room types |
| dim_date.csv | 92 | Date info with week number and day type |
| fact_bookings.csv | 1,34,590 | Individual booking transactions |
| fact_aggregated_bookings.csv | 9,200 | Bookings aggregated by property and room |
| new_data_august.csv | 7 | August 2022 additional data |

**Cities covered:** Delhi, Mumbai, Bangalore, Hyderabad  
**Booking platforms:** Direct Online, Direct Offline, MakeYourTrip, LogTrip, Tripster, Journey, Others

## Data Cleaning

The raw data had several issues addressed using Pandas:

**Removed Invalid Records**
- 12 records with negative or zero guest counts (e.g., -3, -17) were removed.
- 6 records where `successful_bookings` exceeded room capacity, which is logically impossible. These records were removed.
- 5 records with unrealistic revenue values (e.g., ₹2.85 crore for one booking) were removed using the **mean + 3 standard deviation** method.

**Imputed Missing Values**
- 2 records in the aggregated bookings table had missing `capacity` values, filled with the median capacity (25 rooms).

**Left As-Is (Intentional)**
- 77,897 records had missing customer ratings. These were not imputed or removed. Analysis was performed only on available ratings where needed.

**Data Type Conversion**
- Date columns were converted to datetime format for proper time-series analysis.

## Data Transformation

After cleaning, I transformed the data to make analysis easier:

- **Created occupancy percentage** – Added a new column `occ_pct` by dividing `successful_bookings` by `capacity`, then multiplied by 100 and rounded to 2 decimals.
- **Merged with room types** – Joined the aggregated bookings table with `dim_rooms` to get room classes (Standard, Elite, Premium, Presidential) in the data frame instead of just RT1, RT2, etc.
- **Merged with hotels** – Included hotel names, categories, and cities in the data frame.
- **Merged with date table** – Added weekday/weekend flags and month-year info for time-based analysis.
- **Appended August data** – Concatenated the new August 2022 data to the main dataframe for a complete picture.

## Key Insights

### Occupancy by Room Type
Presidential rooms had the highest occupancy at 59.28%. All room types were fairly close to each other between 57% and 60%.

| Room Type | Avg Occupancy % |
|-----------|----------------|
| Presidential | 59.28 |
| Premium | 58.03 |
| Elite | 58.01 |
| Standard | 57.89 |

### Occupancy by City
Delhi led with 61.51% occupancy. Bangalore was the lowest at 56.33%.

| City | Avg Occupancy % |
|------|----------------|
| Delhi | 61.51 |
| Hyderabad | 58.12 |
| Mumbai | 57.91 |
| Bangalore | 56.33 |

### Weekday vs Weekend
Weekend occupancy (72.34%) was significantly higher than weekdays (50.88%). This is a clear pattern the business can use for pricing decisions.

### Revenue by City
Mumbai generated the most revenue at Rs. 66.86 Cr despite not having the highest occupancy, suggesting higher room rates there.

| City | Revenue Realized |
|------|----------------|
| Mumbai | Rs. 66.86 Cr |
| Bangalore | Rs. 42.04 Cr |
| Hyderabad | Rs. 32.52 Cr |
| Delhi | Rs. 29.45 Cr |

### Revenue by Property
Atliq Exotica was the top earner at Rs. 32 Cr. Atliq Seasons was at the bottom with Rs. 6.6 Cr.

### Monthly Revenue Trend
May was the strongest month. Revenue dipped in June before recovering slightly in July.

| Month | Revenue |
|-------|---------|
| May 2022 | Rs. 40.84 Cr |
| June 2022 | Rs. 37.72 Cr |
| July 2022 | Rs. 38.99 Cr |

### Average Customer Rating by City

| City | Avg Rating |
|------|------------|
| Delhi | 3.78 |
| Hyderabad | 3.66 |
| Mumbai | 3.65 |
| Bangalore | 3.41 |

## Tech Stack

Python, Pandas, Matplotlib, Jupyter Notebook

---

## How to Run

```bash
git clone https://github.com/vishaaltijare/Atliq_hospitality_EDA.git
cd Atliq_hospitality_EDA
pip install -r requirements.txt
jupyter notebook EDA_project.ipynb
```

---

## Author

Vishaal
[GitHub](https://github.com/vishaaltijare) 
