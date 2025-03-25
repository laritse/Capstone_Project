<p align = "center">
<img src="https://github.com/laritse/Capstone_Project/blob/main/Bike_Share_Image.jpg" width="600" height="300" />
	
# CASE STUDY - How does a bike-share navigate speedy success?

- [Introduction](#introduction)
- [Data Source](#data-source)
- [Data Cleansing](#data-cleansing)
- [Summary of Analysis](#summary-of-analysis)
- [Recommendations](#recommendations)

### INTRODUCTION

SCENARIO

As a junior data analyst working on the marketing analyst team at Cyclistic, a bike-share
company in Chicago. The director of marketing believes the company’s future success
depends on maximizing the number of annual memberships. Therefore, my team wants to
understand how casual riders and annual members use Cyclistic bikes differently. From these insights, my team will design a new marketing strategy to convert casual riders into annual
members. But first, Cyclistic executives must approve my recommendations, so they must be backed up with compelling data insights and professional data visualizations.

BUSINESS TASK: How do annual members and casual riders use Cyclistic bikes differently?

Busineess Questions

1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?



### DATA SOURCE

This data was made available to the public by Motivate International Inc. under this [license](https://divvybikes.com/data-license-agreement). The company in question is fictional and with a different name known as Cyclistic for the purpose of this case study. I have selected 12 months’ worth of data comprising from the 1st of January 2023 – 31st of December 2023. These Datasets can be found [here](https://divvy-tripdata.s3.amazonaws.com/index.html).

Considering that these datasets were compiled by the company and made available to the public, it is presumed to be credible as it is first-party data.

Datasets were organized and compiled on a monthly basis, making it easy to uncover insights and identify trends 

Note that as a result of Data-privacy issues, personally identifiable information were not provided as such is prohibited.


### DATA CLEANSING

Cleaning Tools
- Google Bigquery

Firstly, considering Dataset was very large, with over 5 million rows and required a tool capable of managing same, I considered Google BigQuery as a perfect tool for processing, easy data manipulation and analysis.

Data was riddled with errors and required cleaning using BigQuery. For proper analysis, I was required to remove errors contained in the data.  This was done by checking for duplicates, standardizing date and time formats, correcting naming inconsistencies and removal of null values from same. To view my data cleaning and manipulation via same, click [here](Data_Cleansing.md)

Visualisation tools

- Tableau

The above was used to create a visual representation of the data and communicate insights and trend patterns. 



### SUMMARY OF ANALYSIS



The following insights and visualizations can provide answers to the business question.



![image alt](https://github.com/laritse/Capstone_Project/blob/81cd741a3a5b14a9eae024cdb06fbbf8e920075e/Report%20Visualizations/Member_dashboard.png)


![image alt](https://github.com/laritse/Capstone_Project/blob/81cd741a3a5b14a9eae024cdb06fbbf8e920075e/Report%20Visualizations/Casual_riders_dashboard.png)


1. #### Most Active Users 

The total number of riders amounts to 5.6 million. Out of this stated number, Members appear to be the most active with a total of 3.6 million riders, and also having a greater percentage of riders at 64% in comparison to Casual riders that accounts for 2 million and a lower rider percentage at 36%. 

2. #### Bike Preference

The difference in bike preference is evident from both dashboards. Members use classic and electric bikes equally. However, Casual riders have greater preference for electric bikes in comparison to traditional classic bikes.

3. #### Trip Duration

Trip duration amongst user types are quite significant, with members having an averge trip of 12.15 Mins and Casual riders having an average of 20.91 Mins. This may suggest Casual riders commute the longest.

4. #### Active Days

The total daily ride distribution gives user insights into their most active and least active days. The ride numbers for Members are at the highest on weekdays. The increase in ride numbers range from 485K to 578K, however at weekends there is a decline in ride numbers, falling to 401k. 
This is the opposite for Casual riders with an increase in demand at weekends, ranging from 329k up to 402k. However on weekdays, there is a decline in ride numbers, falling to 230K. This may suggest Members are more active on weekdays, and Casual Riders are most active at weekends.

5. #### Hourly Ride Trends

Hourly trends differ greatly with both users. Members are in demand from the hours of 7am and 8am. However at 9am there is a drop in demand until the hours of 3pm, with more significant increase in demand at 4pm, and 5pm. For Casual riders, there is a steady increase in demand from the hours of 7am and 8am up until 5pm. The Peak periods for Members may suggest commutes to, and from work. Moreso, considering Casual Riders are in constant demand for bikes, this may suggest Casual riders not only commute to, and from work with the bikes, but increasingly use same for other activities.

6. #### Seasonal Ride Frequencies

Ride trends are similar for both user types in seasonal periods, with Summer having the heaviest demands in bikes, and winter having the least demands in bikes. This is also synonymous with seasonal months as a difference in number of rides and trip duration is evident on both dashboards. This may suggest seasonal periods may impact ride numbers.

For more insights, access to the dashboard can be found [here](https://public.tableau.com/app/profile/ola.beji/viz/CyclisticUserDashboard/MemberDashboard)

In light of the findings above, below are my recommendations

### RECOMMENDATIONS
---
1.	Create a membership plan that specifically caters to needs of casual riders. An example would be a plan designed to focus or cover routes frequently visited by casual riders. 

2.	Considering causal riders have a high preference for e-bikes, and also make long commutes. Offer discounted ride rates on e-bikes, or apply free minutes to same on specific days and times. A good example of this can be drawn from average trip length per day of week, where we saw that on average, days with longer trips were; Sunday, Monday, Friday, and Saturday. In such situation, encourage causal riders with discounts or free minutes on such days.

3.	The use of digital media to influence casual rider’s decisions by means of creating engaging content consistently through owned media such as blogs, websites and social media platforms. 

Secondly, use of paid media such as investing in ad spaces to generate awareness. 

Note: For effective marketing strategy, ad focus should target seasons with increased ride demands based on analysis.





