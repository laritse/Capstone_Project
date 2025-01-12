<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Bike_Share_Image.jpg" width="800" height="500" />
	
# CASE STUDY - How does a bike-share navigate speedy success?

SCENARIO
---
As a junior data analyst working on the marketing analyst team at Cyclistic, a bike-share
company in Chicago. The director of marketing believes the company’s future success
depends on maximizing the number of annual memberships. Therefore, your team wants to
understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual
members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.


### PHASE 1: ASK

BUSINESS TASK: How do annual members and casual riders use Cyclistic bikes differently?

Busineess Questions

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

### PHASE 2: PREPARE

Data Source

This data was made available to the public by Motivate International Inc. under this [license](https://divvybikes.com/data-license-agreement). The company in question is fictional and with a different name known as Cyclistic for the purpose of this case study. I have selected 12 months’ worth of data comprising from the 1st of January 2023 – 31st of December 2023. These Datasets can be found [here](https://divvy-tripdata.s3.amazonaws.com/index.html).

Considering that these datasets were compiled by the company and made available to the public, it is presumed to be credible as it is first-party data.

Datasets were organized and compiled on a monthly basis, making it easy to uncover insights and identify trends 

Note that as a result of Data-privacy issues, personally identifiable information were not provided as such is prohibited.


### PHASE 3: PROCESS

Cleaning Tools

Dataset was very large, with over 5 million rows and required a tool capable of managing same. I considered Google BigQuery as a perfect tool for processing, easy data manipulation and analysis.

Data was riddled with errors and required cleaning using BigQuery. To view my data cleaning and manipulation via same, click here

Visualisation tools

Tableau was used to create a visual representation of the data and communicate insights and trend patterns. Click [here] for visualization and dashboard

PHASE 4: ANALYZE AND SHARE

For proper analysis, I was required to remove errors contained in the data.  This was done by checking for duplicates, standardizing data and time formats, correcting naming inconsistencies and removal of null values from same.


In order to illustrate how casual riders and annual members use Cyclistic bike-share differently, I created a visualization to effectively communicate this. The dashboard viz can be accessed [here].

The following are insights from my analysis and visualization that can provide answers to the business question.


1.	Customer Ride Distribution 
<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Customer_ride_distribution.png" width="450" height="300" />

From the visualization above, we see that there is a huge difference in total bike rides by user type, with members having a total of 3,587,482 rides, in comparison to casual riders that have a total of 2,017,458 rides. This suggest that members use Cyclistic bike-share more often than casual riders.


2.	Ride Hours and Peak Points

<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Ride_Hours.png" width="450" height="300" />


From the above, we can see that the demand in bikes varies amongst user type. For annual members, there is an increase in demand for bikes at 8am and 5pm. However, this is not the case with casual riders, as peak times begin at 12pm and 5pm. Moreso, throughout the day, 
there is a steady increase in demand for bikes by casual riders compared to annual members which shows a decrease in demand between the hours of 9 to 10am.

Considering peak times, it is evident that annual members often commute to work with cyclistic bikes compared to casual riders that use same for leisure purpose.

3.	Bike Preference

<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Bike_Preference.png" width="450" height="300" />


We can see that when comparing user bike preference, both differ. 50% of annual members prefer traditional bikes in comparison to electric bikes, which accounts for the remaining 49%. In the case of casual riders, 53% prefer Electric bikes. 

4.	Average Trip Length Per Day of Week/Season


<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Average_Trip_Length.png" width="450" height="300" />
	
<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Average_Trip_Length_Season.png" width="450" height="300" />



The above visualizations represent the average trip length by both user type. It is evident that casual riders make longer trips compared to annual members. We can also see that trip length pattern remains the same during seasonal periods, however colder months (winter) appear to have an effect on casual riders, but not so much on annual members. 



The above diagrams have similar patterns with casual riders having longer trips. In the first visualization, it is evident that all through the week, casual riders make longer commutes, most significantly on Monday, Friday and weekends. However, this is different for annual members as there is barely any change all week. 

In the second visualization, we get more insights on seasonal trip duration. There seem to be a seasonal effect on User Type, and from the above, we can see that hotter months (Summer) appear to have longer trips compared to colder months (Winter) which shows a decrease in ride lengths for both user type, most significantly in casual riders. This suggest that casual riders make the shortest trips in the months of winter. We can also see that although colder months appear to have an effect on both user type, the change in trip length is insignificant on annual members.


5.	Ride distribution Per Season

<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Ride_Distribution_Season.png" width="450" height="300" />


The above visualization displays seasons totalling the most and least rides by each user type. Arranged in hierarchical order, summer appears to have the most rides for both user type, and winter being the season with the least rides. We can see that there is a significant reduction of casual riders in winter compared to annual members. 



6.	User ride end locations


<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Members_Ride_End_Locations.png" width="450" height="300" />

<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Casual_Ride_End_Locations.png" width="450" height="300" />

The above map visualization displays user end locations. The darker the density represents a large volume of commuters. According to the map, annual members are scattered around the map whilst casual riders are concentrated around specific tourist locations. This further suggest that annual members often commute to work with the cyclistic bikes and casual riders use same for leisure purpose.


RECOMMENDATIONS

1.	Creating a membership plan that specifically caters to needs of casual riders. An example would be a plan designed to focus/cover routes frequently visited. 

2.	Considering causal riders have a high demand preference for e-bikes, and make long commutes, offer discounted ride rates on e-bikes, or apply free minutes to same on specific days and times. A good example of this can be drawn from average trip length per day of week, where we saw that on average, days with longer trips were; Sunday, Monday, Friday, and Saturday. In such situation, encourage causal riders with discounts or free minutes on such days.

3.	The use of digital media to influence casual rider’s decisions by means of creating engaging content consistently through owned media such as blogs, websites and social media platforms. 

Secondly, use of paid media such as investing in ad spaces to generate awareness. 

Note: For effective marketing strategy, ad focus should target seasons that produced larger number of rides.





