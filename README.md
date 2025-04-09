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





## How long does a typical bike ride last?

This histogram illustrates the distribution of bike ride durations in one-minute intervals, revealing that the majority of rides are short and highly concentrated below 20 minutes. The plot includes vertical lines marking key statistical measures:

Mode (green): 4.53 minutes – the most frequent ride duration.

Median (blue): 8.37 minutes – the midpoint of all rides.

Mean (red): 9.85 minutes – pulled slightly higher by longer-duration outliers.

Threshold (purple): 78.5 minutes – used to identify unusually long trips.

The data is right-skewed, with a long tail of less frequent, longer rides. This skew highlights that while the average appears close to 10 minutes, the typical trip is actually shorter, closer to 6–8 minutes. The steep drop-off confirms the system is primarily used for short, utilitarian rides, likely for commuting or local errands.

This visualization supports the insight that most users take quick trips, and long rides are rare—key for fleet optimization, trip forecasting, and designing user-centric policies.




### Average Trip Duration by Day and User Type

This bar plot compares the average trip duration across days of the week, split by user type (Subscriber vs. Customer). It clearly highlights the behavioral difference between user types:

Subscribers maintain a steady and shorter ride duration throughout the week, reflecting their consistent use for commuting or quick transport.

Customers have longer trips overall, with a noticeable increase on weekends, suggesting leisure or recreational usage.

The visualization effectively supports the insight that ride purpose varies by user type and day of the week, helping to inform resource planning and marketing strategies for different user groups.



## How does the user type (Customer or Subscriber) affect bike usage?

This dual histogram compares ride duration distributions between Subscribers and Customers, revealing clear differences in bike usage patterns based on user type.

Subscribers show a strong peak between 5–10 minutes, with a steep drop-off after that. This distribution suggests frequent, short rides—characteristic of commute-driven behavior.

Customers, on the other hand, have a flatter, more spread-out distribution, indicating fewer but longer rides. This supports the idea that customers are more likely to be casual or recreational users, such as tourists or occasional riders.

The contrast in volume is also notable—subscribers take significantly more rides overall, which reinforces the system’s role as a commuter tool for regular users, while customers represent a smaller, more leisurely segment.

This visualization directly supports one of the core insights: user type significantly impacts both frequency and duration of bike usage, and different strategies should be used to serve each segment effectively.



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



###  Top Destinations for Bike Rides

This horizontal bar chart displays the top 5 most common bike ride destinations within the Ford GoBike system, based on the number of trips ending at each station.

San Francisco Caltrain Station 2 (Townsend St at 4th St) stands out as the most frequented destination, reinforcing its role as a critical last-mile connection point for commuters using regional transit.

Other high-traffic destinations include:Market St at 10th St, Montgomery St BART Station (Market St at 2nd St), San Francisco Ferry Building (Harry Bridges Plaza), San Francisco Caltrain (Townsend St at 4th St)

All five are strategically located near public transportation hubs or dense business districts, confirming the bike-share system’s integration into urban mobility.




## Median Trip Duration by Gender and Top Destination

This heatmap presents the median trip duration (in seconds) across the top 5 most common destination stations, segmented by gender. It provides a side-by-side comparison of how ride lengths vary between female, male, and other riders depending on the end station.

Across almost all destinations, female riders tend to have longer median trip durations than male riders.

For example, at Montgomery St BART Station, the median duration for female users is 668 seconds (11.1 minutes), compared to 531.5 seconds (8.9 minutes) for males.

The Ferry Building and Market St also show higher durations for females and other users.

The most balanced distribution appears at San Francisco Caltrain Station 2, but even there, male riders record shorter average durations.




    
![png](output_21_0.png)
    
