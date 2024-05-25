# Delhi-Metro-Network-Analysis-using-Python

## Overview
This project involves analyzing the Delhi Metro network using Python to understand its structure, efficiency, and effectiveness. The analysis includes examining routes, stations, traffic, and connectivity.

## Prerequisites
- Python 3.x
- Pandas
- Folium
- Plotly

## Setup
1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/delhi-metro-analysis.git
   cd delhi-metro-analysis
   ```
2. **Install the required libraries**:
   ```bash
   pip install pandas folium plotly
   ```

## Data
Download the dataset from [here](https://statso.io).

## Steps

### 1. Data Loading and Cleaning
```python
import pandas as pd

metro_data = pd.read_csv("Delhi Metro Network.csv")
metro_data['Opening Date'] = pd.to_datetime(metro_data['Opening Date'])
```

### 2. Geospatial Analysis
Visualize the locations of metro stations on a map.
```python
import folium

delhi_map = folium.Map(location=[28.7041, 77.1025], zoom_start=11)
for _, row in metro_data.iterrows():
    folium.Marker(
        location=[row['Latitude'], row['Longitude']],
        popup=row['Station Name'],
        tooltip=f"{row['Station Name']}, {row['Line']}",
        icon=folium.Icon(color='blue')
    ).add_to(delhi_map)
delhi_map.save('delhi_metro_map.html')
```

### 3. Temporal Analysis
Analyze the growth of the metro network over time.
```python
metro_data['Opening Year'] = metro_data['Opening Date'].dt.year
stations_per_year = metro_data['Opening Year'].value_counts().sort_index()
stations_per_year.plot(kind='bar', title='Number of Metro Stations Opened Each Year')
```

### 4. Line Analysis
Examine the number of stations and average distance between stations for each line.
```python
stations_per_line = metro_data['Line'].value_counts()
avg_distance_per_line = metro_data.groupby('Line')['Distance from Start (km)'].mean()
```

### 5. Station Layout Analysis
Analyze the distribution of different station layouts.
```python
layout_counts = metro_data['Station Layout'].value_counts()
layout_counts.plot(kind='bar', title='Distribution of Station Layouts')
```

## Visualizations
- **Map of Delhi Metro Stations**: `delhi_metro_map.html`
- **Bar Chart of Stations per Year**
- **Bar Chart of Line Analysis**
- **Bar Chart of Station Layout Distribution**

## Conclusion
This project provides a comprehensive analysis of the Delhi Metro network, offering insights into its geographical distribution, temporal growth, line characteristics, and station layouts.

```
