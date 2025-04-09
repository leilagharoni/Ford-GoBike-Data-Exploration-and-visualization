# Ford-GoBike-Data-Exploration-and-visualization
# Ford GoBike Data Explanatory(Part 2)
# by Leila Gharoni

## Table of Content
<ul>
    <li><a href="#IN">1. Investigation Overview</a></li>
    <li><a href="#DO">2. Dataset Overview</a></li>
    <li><a href="#KI">3. Key Insight</a></li>
   
</ul>

<a id='IN'></a> 
## Investigation Overview

This investigation analyzes Ford GoBike (bike-sharing system) data. The primary objective is to uncover behavioral and operational trends based on time, user type, gender, and location. These insights aim to support smarter operational planning, enhance user experience, and inform infrastructure improvements.

The analysis is organized into three main focus areas:

####  Time-Related Characteristics

. How long does a typical bike ride last?
Explores trip duration distributions to identify averages, medians, and outliers.

. Average Trip Duration by Day and User Type: 
This analysis explores how ride durations vary across different days of the week and how these patterns differ between Subscribers and Customers. The goal is to understand whether ride lengths are influenced by weekday vs. weekend behavior and how this is shaped by the type of user.

#### User-Related Characteristics

. How does the user type (Customer or Subscriber) affect bike usage?
Compares ride frequency, duration, and patterns across user types to distinguish between commuter and casual behavior.

. Hourly Bike Usage by Gender and Day of Week: 
Analyzes usage peaks by hour of day for each gender, identifying daily patterns and differences between weekdays and weekends.

#### Location-Related Insights

. Top Destinations for Bike Rides: 
Identifies the most frequently used end stations and examines their connection to public transit and business hubs.

. Median Trip Duration by Gender and Top Destination: 
Highlights differences in ride behavior by gender at high-traffic stations to understand infrastructure and equity implications.

<a id='DO'></a> 
## Dataset Overview

This project explores a dataset from the Ford GoBike bike-sharing system, capturing 174,952 individual trips taken between February 1 and March 1, 2019. Each record includes information such as trip duration, start and end times, start and end stations, user type (Customer or Subscriber), and gender. The goal of this investigation is to uncover patterns in bike usage related to time, user demographics, and location, and to provide data-driven insights for improving system efficiency and user experience.

<a id='KI'></a> 
### Key Insights

1. Most rides are short and commute-driven, with 50% lasting between 5 to 13 minutes and peaking during weekday morning and evening rush hours.

2. Subscribers dominate ridership, taking shorter, more frequent trips—especially during commuting hours—while Customers ride less often but for longer durations, particularly on weekends.

3. Thursdays are the busiest day, followed by Tuesday and Wednesday, indicating strong weekday commuter usage. Weekends see fewer but longer rides.

4. The top destination is San Francisco Caltrain Station 2, reflecting its importance as a last-mile connection point to regional transit.

5. Ride behavior varies by gender: female riders tend to have slightly longer trips, while male riders make up the majority of overall rides.

6. Across all genders, weekday riding shows a clear dual-peak pattern (commute times), while weekend rides peak midday, suggesting recreational usage.

7. High-usage stations are clustered around transit and business hubs, confirming the system’s strong role in supporting short, urban mobility.

These findings are supported by a series of visualizations that analyze temporal usage patterns, user demographics, and geographic trends within the system.


```python
# import all packages and set plots to be embedded inline
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# suppress warnings from final output
import warnings
warnings.simplefilter("ignore")
```


```python
# load in the dataset into a pandas dataframe
df = pd.read_csv("fordgobike-tripdata-clean.csv")
```


```python
# Cleaning Outliers
quartiles = np.percentile(df['duration_min'], [25, 50, 75])
mu = quartiles[1]
sig = 0.74 * (quartiles[2] - quartiles[0])
df1= df.query('(duration_min > @mu - 5 * @sig) & (duration_min < @mu + 5 * @sig)')
```


```python
df1.describe()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>duration_sec</th>
      <th>start_station_id</th>
      <th>start_station_latitude</th>
      <th>start_station_longitude</th>
      <th>end_station_id</th>
      <th>end_station_latitude</th>
      <th>end_station_longitude</th>
      <th>bike_id</th>
      <th>member_birth_year</th>
      <th>start_year</th>
      <th>start_hr</th>
      <th>end_hr</th>
      <th>duration_min</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.0</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
      <td>171317.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>591.042985</td>
      <td>138.612712</td>
      <td>37.771095</td>
      <td>-122.351498</td>
      <td>135.960033</td>
      <td>37.771286</td>
      <td>-122.351031</td>
      <td>4478.271567</td>
      <td>1984.819358</td>
      <td>2019.0</td>
      <td>13.447731</td>
      <td>13.587928</td>
      <td>9.850716</td>
    </tr>
    <tr>
      <th>std</th>
      <td>373.426333</td>
      <td>111.144681</td>
      <td>0.100637</td>
      <td>0.117917</td>
      <td>110.684689</td>
      <td>0.100537</td>
      <td>0.117450</td>
      <td>1661.291088</td>
      <td>10.088808</td>
      <td>0.0</td>
      <td>4.747431</td>
      <td>4.755848</td>
      <td>6.223772</td>
    </tr>
    <tr>
      <th>min</th>
      <td>61.000000</td>
      <td>3.000000</td>
      <td>37.317298</td>
      <td>-122.453704</td>
      <td>3.000000</td>
      <td>37.317298</td>
      <td>-122.453704</td>
      <td>11.000000</td>
      <td>1878.000000</td>
      <td>2019.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>1.016667</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>319.000000</td>
      <td>49.000000</td>
      <td>37.770083</td>
      <td>-122.411738</td>
      <td>44.000000</td>
      <td>37.770407</td>
      <td>-122.411403</td>
      <td>3792.000000</td>
      <td>1980.000000</td>
      <td>2019.0</td>
      <td>9.000000</td>
      <td>9.000000</td>
      <td>5.316667</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>502.000000</td>
      <td>104.000000</td>
      <td>37.780760</td>
      <td>-122.398279</td>
      <td>100.000000</td>
      <td>37.781010</td>
      <td>-122.397405</td>
      <td>4959.000000</td>
      <td>1987.000000</td>
      <td>2019.0</td>
      <td>14.000000</td>
      <td>14.000000</td>
      <td>8.366667</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>766.000000</td>
      <td>239.000000</td>
      <td>37.797320</td>
      <td>-122.283093</td>
      <td>233.000000</td>
      <td>37.797320</td>
      <td>-122.285171</td>
      <td>5504.000000</td>
      <td>1992.000000</td>
      <td>2019.0</td>
      <td>17.000000</td>
      <td>18.000000</td>
      <td>12.766667</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2234.000000</td>
      <td>398.000000</td>
      <td>37.880222</td>
      <td>-121.874119</td>
      <td>398.000000</td>
      <td>37.880222</td>
      <td>-121.874119</td>
      <td>6645.000000</td>
      <td>2001.000000</td>
      <td>2019.0</td>
      <td>23.000000</td>
      <td>23.000000</td>
      <td>37.233333</td>
    </tr>
  </tbody>
</table>
</div>




```python
df1.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>duration_sec</th>
      <th>start_time</th>
      <th>end_time</th>
      <th>start_station_id</th>
      <th>start_station_name</th>
      <th>start_station_latitude</th>
      <th>start_station_longitude</th>
      <th>end_station_id</th>
      <th>end_station_name</th>
      <th>end_station_latitude</th>
      <th>...</th>
      <th>member_gender</th>
      <th>bike_share_for_all_trip</th>
      <th>start_day</th>
      <th>start_month</th>
      <th>start_year</th>
      <th>start_hr</th>
      <th>end_day</th>
      <th>end_month</th>
      <th>end_hr</th>
      <th>duration_min</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>3</th>
      <td>1585</td>
      <td>2019-02-28 23:54:18.549</td>
      <td>2019-03-01 00:20:44.074</td>
      <td>7.0</td>
      <td>Frank H Ogawa Plaza</td>
      <td>37.804562</td>
      <td>-122.271738</td>
      <td>222.0</td>
      <td>10th Ave at E 15th St</td>
      <td>37.792714</td>
      <td>...</td>
      <td>Male</td>
      <td>Yes</td>
      <td>Thursday</td>
      <td>February</td>
      <td>2019</td>
      <td>23</td>
      <td>Friday</td>
      <td>March</td>
      <td>0</td>
      <td>26.416667</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1793</td>
      <td>2019-02-28 23:49:58.632</td>
      <td>2019-03-01 00:19:51.760</td>
      <td>93.0</td>
      <td>4th St at Mission Bay Blvd S</td>
      <td>37.770407</td>
      <td>-122.391198</td>
      <td>323.0</td>
      <td>Broadway at Kearny</td>
      <td>37.798014</td>
      <td>...</td>
      <td>Male</td>
      <td>No</td>
      <td>Thursday</td>
      <td>February</td>
      <td>2019</td>
      <td>23</td>
      <td>Friday</td>
      <td>March</td>
      <td>0</td>
      <td>29.883333</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1147</td>
      <td>2019-02-28 23:55:35.104</td>
      <td>2019-03-01 00:14:42.588</td>
      <td>300.0</td>
      <td>Palm St at Willow St</td>
      <td>37.317298</td>
      <td>-121.884995</td>
      <td>312.0</td>
      <td>San Jose Diridon Station</td>
      <td>37.329732</td>
      <td>...</td>
      <td>Female</td>
      <td>No</td>
      <td>Thursday</td>
      <td>February</td>
      <td>2019</td>
      <td>23</td>
      <td>Friday</td>
      <td>March</td>
      <td>0</td>
      <td>19.116667</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1615</td>
      <td>2019-02-28 23:41:06.766</td>
      <td>2019-03-01 00:08:02.756</td>
      <td>10.0</td>
      <td>Washington St at Kearny St</td>
      <td>37.795393</td>
      <td>-122.404770</td>
      <td>127.0</td>
      <td>Valencia St at 21st St</td>
      <td>37.756708</td>
      <td>...</td>
      <td>Male</td>
      <td>No</td>
      <td>Thursday</td>
      <td>February</td>
      <td>2019</td>
      <td>23</td>
      <td>Friday</td>
      <td>March</td>
      <td>0</td>
      <td>26.916667</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1570</td>
      <td>2019-02-28 23:41:48.790</td>
      <td>2019-03-01 00:07:59.715</td>
      <td>10.0</td>
      <td>Washington St at Kearny St</td>
      <td>37.795393</td>
      <td>-122.404770</td>
      <td>127.0</td>
      <td>Valencia St at 21st St</td>
      <td>37.756708</td>
      <td>...</td>
      <td>Other</td>
      <td>No</td>
      <td>Thursday</td>
      <td>February</td>
      <td>2019</td>
      <td>23</td>
      <td>Friday</td>
      <td>March</td>
      <td>0</td>
      <td>26.166667</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 24 columns</p>
</div>



## How long does a typical bike ride last?

This histogram illustrates the distribution of bike ride durations in one-minute intervals, revealing that the majority of rides are short and highly concentrated below 20 minutes. The plot includes vertical lines marking key statistical measures:

Mode (green): 4.53 minutes – the most frequent ride duration.

Median (blue): 8.37 minutes – the midpoint of all rides.

Mean (red): 9.85 minutes – pulled slightly higher by longer-duration outliers.

Threshold (purple): 78.5 minutes – used to identify unusually long trips.

The data is right-skewed, with a long tail of less frequent, longer rides. This skew highlights that while the average appears close to 10 minutes, the typical trip is actually shorter, closer to 6–8 minutes. The steep drop-off confirms the system is primarily used for short, utilitarian rides, likely for commuting or local errands.

This visualization supports the insight that most users take quick trips, and long rides are rare—key for fleet optimization, trip forecasting, and designing user-centric policies.



```python
import statistics

# Define the data
graph = df1['duration_min']

# Create 1-minute bins from 0 to the next whole number after the max duration
bins = np.arange(0, int(graph.max()) + 2, 1)

# Set figure size
plt.figure(figsize=(12, 6))

# Plot histogram
plt.hist(graph, bins=bins, edgecolor='black')
plt.xlim(0, 100)

# Axis labels and title
plt.xlabel('Ride Duration (1-minute bins)', fontsize=12)
plt.ylabel('Number of Rides', fontsize=12)
plt.title('How Long Does a Typical Bike Ride Last?', fontsize=16)

# Add vertical lines for statistical measures
mean_val = statistics.mean(graph)
mode_val = statistics.mode(graph)
median_val = statistics.median(graph)

plt.axvline(mean_val, color='red', linestyle='--', linewidth=2, label=f'Mean: {mean_val:.2f} min')
plt.axvline(mode_val, color='green', linestyle='--', linewidth=2, label=f'Mode: {mode_val:.2f} min')
plt.axvline(median_val, color='blue', linestyle='--', linewidth=2, label=f'Median: {median_val:.2f} min')
plt.axvline(78.5, color='purple', linestyle='--', linewidth=2, label='Threshold: 78.5 min')

# Add legend
plt.legend()

# Show plot
plt.tight_layout()
plt.show()
```


    
![png](output_11_0.png)
    


### Average Trip Duration by Day and User Type

This bar plot compares the average trip duration across days of the week, split by user type (Subscriber vs. Customer). It clearly highlights the behavioral difference between user types:

Subscribers maintain a steady and shorter ride duration throughout the week, reflecting their consistent use for commuting or quick transport.

Customers have longer trips overall, with a noticeable increase on weekends, suggesting leisure or recreational usage.

The visualization effectively supports the insight that ride purpose varies by user type and day of the week, helping to inform resource planning and marketing strategies for different user groups.


```python
# Set seaborn style
sns.set(style='whitegrid')

plt.figure(figsize=(8, 5))

# Define the weekday order
weekday = ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
weekdaycat = pd.api.types.CategoricalDtype(ordered=True, categories=weekday)

# Ensure 'start_day' is treated as a categorical variable with the defined order
df1['start_day'] = df1['start_day'].astype(weekdaycat)

# Create the bar plot
sns.barplot(data=df1, x='start_day', y='duration_min', hue='user_type')

# Add labels and title
plt.xlabel('Day of the Week', fontsize=12)
plt.ylabel('Ride Duration (minutes)', fontsize=12)
plt.title("How Trip Duration Varies by Day and User Type", fontsize=16)
plt.legend(title='User Type')

# Display the plot
plt.tight_layout()
plt.show()
```


    
![png](output_13_0.png)
    


## How does the user type (Customer or Subscriber) affect bike usage?

This dual histogram compares ride duration distributions between Subscribers and Customers, revealing clear differences in bike usage patterns based on user type.

Subscribers show a strong peak between 5–10 minutes, with a steep drop-off after that. This distribution suggests frequent, short rides—characteristic of commute-driven behavior.

Customers, on the other hand, have a flatter, more spread-out distribution, indicating fewer but longer rides. This supports the idea that customers are more likely to be casual or recreational users, such as tourists or occasional riders.

The contrast in volume is also notable—subscribers take significantly more rides overall, which reinforces the system’s role as a commuter tool for regular users, while customers represent a smaller, more leisurely segment.

This visualization directly supports one of the core insights: user type significantly impacts both frequency and duration of bike usage, and different strategies should be used to serve each segment effectively.




```python
# Set up the FacetGrid for user type comparison
g = sns.FacetGrid(df1, col='user_type', col_wrap=2, height=5, sharex=True, sharey=True)

# Define bin size 
bins = np.arange(df1['duration_min'].min(), df1['duration_min'].max() +2, 2)

# Plot histogram with improved aesthetics
g.map(plt.hist, 'duration_min', bins=bins, edgecolor='black', alpha=0.7)

# Label axes and set subplot titles
g.set_axis_labels('Ride Duration (minutes)', 'Number of rides')
g.set_titles(col_template="{col_name}")

# Adjust layout and add a main title
plt.subplots_adjust(top=0.85)
g.fig.suptitle('How does user type affect bike usage?', fontsize=10, fontweight='bold')

# Show the plot
plt.show()

```


    
![png](output_15_0.png)
    


## Hourly Bike Usage by Gender and Day of Week

This multi-panel histogram shows bike usage by hour of day, segmented by both day of the week (columns) and gender (rows: Male, Female, Other). It captures clear temporal usage patterns across user demographics.

Weekdays (Monday–Friday):
All genders show dual peaks around 8 AM and 5 PM, aligning with standard commute hours.
Male riders dominate in volume, with consistent usage throughout the week.
Female riders follow similar patterns, though with slightly lower counts.

Weekends (Saturday–Sunday):
A shift to a single midday peak (11 AM – 2 PM) across all genders.

Suggests increased recreational or casual use outside of work hours.

Gender Comparison:
Although overall volume is lower for Female and Other users, their behavior mirrors male riders in terms of peak timing.

The “Other” gender group shows minimal usage but still follows a similar trend structure, indicating uniform behavioral rhythms across gender identities.


```python
# Define hourly bins (0 to 24)
bins = np.arange(0, 25, 1)

# Create FacetGrid
g = sns.FacetGrid(data=df1, col="start_day", row="member_gender", margin_titles=True, sharey=False, height=3)

# Map histogram
g.map(plt.hist, 'start_hr', bins=bins, edgecolor='black')

# Add axis labels
g.set_axis_labels("Hour of Day", "Number of Rides")

# Add custom titles
g.set_titles(col_template="{col_name}", row_template="{row_name}")

# Add a main title
g.fig.subplots_adjust(top=0.9)
g.fig.suptitle("Hourly Bike Usage by Gender and Day of Week", fontsize=16)

plt.show()
```


    
![png](output_17_0.png)
    


###  Top Destinations for Bike Rides

This horizontal bar chart displays the top 5 most common bike ride destinations within the Ford GoBike system, based on the number of trips ending at each station.

San Francisco Caltrain Station 2 (Townsend St at 4th St) stands out as the most frequented destination, reinforcing its role as a critical last-mile connection point for commuters using regional transit.

Other high-traffic destinations include:Market St at 10th St, Montgomery St BART Station (Market St at 2nd St), San Francisco Ferry Building (Harry Bridges Plaza), San Francisco Caltrain (Townsend St at 4th St)

All five are strategically located near public transportation hubs or dense business districts, confirming the bike-share system’s integration into urban mobility.


```python
# Get the top 5 most common destination stations
top_dst = df1['end_station_name'].value_counts().nlargest(5).index

# Filter the dataframe to include only trips to those top 5 destinations
top_dst_df = df1[df1['end_station_name'].isin(top_dst)]

# Set plot style and figure size
sns.set_style('darkgrid')
plt.figure(figsize=(12, 5))

# Count and sort the destinations for plotting
top_counts = top_dst_df['end_station_name'].value_counts().sort_values(ascending=True)

# Create the horizontal bar chart
top_counts.plot(kind='barh', color='skyblue', edgecolor='black')

# Add labels and title
plt.title('Top Destinations for Bike Rides', fontsize=16)
plt.xlabel('Number of Rides', fontsize=12)
plt.ylabel('End Station Name', fontsize=12)
plt.tight_layout()

# Show plot
plt.show()
```


    
![png](output_19_0.png)
    


## Median Trip Duration by Gender and Top Destination

This heatmap presents the median trip duration (in seconds) across the top 5 most common destination stations, segmented by gender. It provides a side-by-side comparison of how ride lengths vary between female, male, and other riders depending on the end station.

Across almost all destinations, female riders tend to have longer median trip durations than male riders.

For example, at Montgomery St BART Station, the median duration for female users is 668 seconds (11.1 minutes), compared to 531.5 seconds (8.9 minutes) for males.

The Ferry Building and Market St also show higher durations for females and other users.

The most balanced distribution appears at San Francisco Caltrain Station 2, but even there, male riders record shorter average durations.


```python
# Set figure size
plt.figure(figsize=(15, 6))

# Group by gender and top destination, then calculate the median duration
cat_means = top_dst_df.groupby(['member_gender', 'end_station_name']).median(numeric_only=True)['duration_sec'].reset_index()

# Pivot the table to create a matrix suitable for a heatmap
cat_means = cat_means.pivot(index='end_station_name', columns='member_gender', values='duration_sec')

# Plot heatmap
sns.heatmap(cat_means, annot=True, fmt=".1f", cmap="YlGnBu", cbar_kws={"label": "Median Duration (seconds)"})

# Label axes
plt.xlabel("Gender")
plt.ylabel("Top Destination")
plt.title("Median Trip Duration by Gender and Top Destination", fontsize=14)

plt.tight_layout()
plt.show()
```


    
![png](output_21_0.png)
    
