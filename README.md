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


