# Cyclistic
Cyclistic bike share analysis.

## About the Company: **Cyclistic**

A bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can’t use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use the bikes to commute to work each day.

The director of marketing and your manager, Moreno is responsible for the development of campaigns and initiatives to promote the bike-share program. These may include email, social media, and other channels.

**Scenario:**

The director of marketing believes the company’s future success depends on maximizing the number of annual memberships. Therefore, your team wants to understand how casual riders and annual members use Cyclistic bikes differently. From these insights, your team will design a new marketing strategy to convert casual riders into annual members. But first, Cyclistic executives must approve your recommendations, so they must be backed up with compelling data insights and professional data visualizations.

**Objective:**

Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends.

# The Data Analysis Process

## I. Ask — Defining the problem

These three questions will guide the future marketing program:

How do annual members and casual riders use Cyclistic bikes differently?

Why would casual riders buy Cyclistic annual memberships?

How can Cyclistic use digital media to influence casual riders to become members?

Our first business task is to identify *how annual members and casual riders use Cyclistic bikes differently*. Understanding how these two different customer profiles interact with the company’s offerings is key to designing effective marketing strategies that convert casual riders to annual memberships while using data to drive these decisions and fuel the company’s future growth.

## II. Prepare — Data collection

We will be using Cyclistic’s historical trip data to analyze and identify trends. The dataset that we are using contains CSV files that details every ride logged from Cyclistic customers .For the purpose of this case study, we will be focusing on data from the previous 12 months, January 2024 to December 2024. The data has been made available by Motivate International Inc. under this license.

The data is organized into rows and columns with ride_id as the unique identifier for each trip. The data includes the following 13 fields:
|data type  | description|
|---------  | -------------|
| ride_id | unique identifier for logged rides |
| rideable_bike | type of bike (classic, docked, electric)|
| started_at | the date and time in which the ride started (M/d/yyyy hh:mm) |
| ended_at | the date and time in which the ride ended (M/d/yyyy hh:mm) |
| start_station_name  | the station name where the ride started|
| start_station_id | the id for the start station |
| end_station_name | the station name where the ride ended |
| end_station_id | the id for the end station |
| start_lat | the latitude of the starting station |
| start_lng | the longitude of the starting station |
| end_lat | the latitude of the ending station |
| end_lng | the longitude of the ending station |
| member_casual | the type of rider (member, casual) |

## III. Process — Cleaning and manipulating the data

Processing data is extremely important in ensuring that the data that we want to analyze is consistent and free of errors so that the insights that we generate are accurate and useful for us to make effective decisions.
Our first course of action is to download the zip files for the past 12 months, organize them into folders and subfolders using appropriate naming conventions, and convert the formatting of each .CSV file to .XLSX so that we have an original copy of our data.
Then I opened all the files in **Excel** to process by cleaning .

* I checked whether all the 12 files have the same number of columns and datatypes.
* I confirmed that the ride_id column has 16 letters as its the unique identifier of the data. I used LEN() function to do that.
* I deleted all the rows that has NULL values. Mostly deleted the rows that were empty in Start_station_name and End_station_name . Used filter to remove all the blank rows.
* Created a separate column for start and end date as both the columns were having start and end date& time in a same cell.=INT() function will extract the date from the timestamp cell
* Created a separate column for fetching the day of the week from the date cell . Weekday() function will get the day of the week from the date column.
* Extracted the start and end time from the date&timestamp cell.C1-INT(C1) will extract the time from the cell.
* Changed the time format into HH:MM:SS
* Checked for the duplicates . I didn’t find any duplicates in these files.
* I repeated all the above steps for all the 12 month files. Now the data is cleaned and ready for analyzing.

## IV. Analyze — Identifying the patterns

After cleaning i got the total number of rides as 4,208,041
I have used my **SQL big query** for my analyzing process as the data is huge.
I have uploaded all my 12 files in the SQL Big query under my project. For further more analyzing i thought of combining all the 12 files into a single table to do it.
I have analyzed the following using the SQL queries

* Total number of rides by rideable type
* Number of rides by member or casual depending upon their ride type
* Number of rides by member and casual
* Number of rides by each month
* Number of rides by hour
* Number of rides by week
* Average trip duration
* Avg trip duration by rideable type and day of the week
* Top 10 start station name for members
* Top 10 start station name for casual
* Highest number of rides between two stations
  
### Total number of rides by rideable type

I got the total number of rides by the rideable type to know which one is the most favorite for both member as well as casual users . Classic bike is mostly used followed by electric bike and electric scooter is least used.

![Total number of rides by rideable type1](https://github.com/user-attachments/assets/5cade55f-04da-425b-945d-f6089748a38d)



### Total number of rides by member/casual by their rideable type

Since we found that the classic bike is mostly used , I wanted to find who used the classic bike more whether it is member or casual bike riders

![Number of rides by member or casual depending upon their ride type](https://github.com/user-attachments/assets/8e35a3bb-5efa-4df0-bdf6-2e40a2e45b10)



From the above visual we got to know that both member and casual riders used the classic bike more often for their rides.

*casual riders percentage*

63.67% of riders use classic bike , 34.63% uses electric bike and 1.69% uses electric scooter

*Member riders percentage*

65.48% of riders use classic bike , 33.70% uses electric bike and 0.82% uses electric scooter

When taking the specific population of member and casual riders , members preferred classic bike more than the casual riders where as casual riders preferred electric bike and electric scooter more than the members for their rides.

### Number of rides by member and casual riders


Among the total number of riders 4,208,041 , 63.84%(2,686,574) were members and 36.16%(1,521,467) were casual riders .

<img width="621" alt="Screenshot (2)" src="https://github.com/user-attachments/assets/4056fb02-fc4c-419f-a95e-7e42add1a535" />



### Number of rides by each month


Our data says that both member and casual riders love to ride their bike during the hottest months of the year i.e. from June to September , where September records the highest number rides for Member and July records the highest number of rides for casual riders.

December and January records the lowest number of rides for both casual and member users.


![Number of rides by each month (11)](https://github.com/user-attachments/assets/0c263793-c998-4a28-aa23-2f4fe0a23e0a)




### Number of rides by hour


*Casual riders*

When we look at the number of rides daily , by hour , casual riders has the highest number of rides at 5pm(146,736 rides) , followed by 4 and 3pm . The number of rides are gradually increasing from 11am to 5pm for casual riders.


<img width="857" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/30671dee-35e1-49af-b607-6327d5ed3899" />




*Members*

When we look at the number of rides daily , by hour , members has the highest number of rides at 5pm.However , members doesn't have gradual increase in their rides .


<img width="862" alt="Screenshot (5)" src="https://github.com/user-attachments/assets/c594d882-8956-4598-946a-3a42923803f7" />




### Number of rides by week

*casual*


When we look at the number of casual rides , they have highest number of rides on Saturday and Sunday . They are riding only on weekends . This answers us why they have the gradual increase of rides from 11am to 5pm . Tuesdays were the least . Casual riders are preferring bike for their weekend getaways.

<img width="819" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/f396881e-610f-4936-8f0d-0dfa240b6fbe" />



*Member*


Members has the highest number of rides on Wednesdays . They have the highest number of rides on weekdays . Members are preferring bike for their official work. This explains us why the number of rides were high during peak hours i.e. from 6am to 8am and from 3pm to 5pm. This is in-line with our analysis on rides by hour.


<img width="739" alt="Screenshot (7)" src="https://github.com/user-attachments/assets/756b433e-d736-41eb-a423-c49d9121de16" />




### Average trip duration


<img width="398" alt="Screenshot (10)" src="https://github.com/user-attachments/assets/2e4fd544-2ed0-469e-8f00-30cf0f7b1f3c" />



*casual*


Casual riders have the highest average trip duration of 28 minutes on Sundays followed by 27 minutes Saturday.


*Member*


Members have the highest average trip duration of 14 minutes on Saturdays and Sundays .



 *Average trip duration in minutes for both casual and member riders along with their bike type*

 

 <img width="819" alt="Avg trip duration by casual member" src="https://github.com/user-attachments/assets/2a473259-974c-4cc3-8835-5cd64efccdd4" />



### Top 10 start station name for members


Kingbury st & Kinzie st were the popular start station among the members having 26,807 rides start from that particular station , which is closely followed by three other stations .

<img width="1206" alt="Screenshot (15)" src="https://github.com/user-attachments/assets/b3f1df55-6741-48ee-bd97-a78a432c1b05" />




### Top 10 start station name for casuals


streeter st &Grand ave were the popular start station among the casuals having 48,314 rides start from that particular station.


<img width="1164" alt="Screenshot (16)" src="https://github.com/user-attachments/assets/69663512-872e-4764-9099-23f297a1f471" />




### Highest number of rides between two stations(Top 10 start and end station names)


The most popular route is To and From Streeter Dr & Grand Ave with 9668 rides , followed by To and From DuSable Lake Shore Dr & Monroe St with 7917 rides.


<img width="925" alt="Screenshot (17)" src="https://github.com/user-attachments/assets/23905b89-e5b0-4ceb-83a9-ce121db5e2f9" />




## V. Share — The art of visualization
Data visualization is the process of graphically representing our data. It is a way to engage our audience and communicate our findings to tell a story that goes beyond the numbers. It is important that we create effective visuals that allow our audience to take in all the information in an easily digestible manner and draws them to have a conversation with the data.

The above visuals are made from Tableau by uploading the required data from the SQL ->Local folder->Tableau

Click here for the detailed visualization-> [My first Tableau dashboard](https://public.tableau.com/app/profile/theepika.gunalan/viz/CyclisticBikeShare_17422294507330/Cyclisticbikeshareanalysis)

## VI. Act — Making data-driven decisions
The final phase in our analysis involves applying our insights to help drive solutions and recommendations that are backed by data. Our business task was to identify how the two different customer groups use Cyclistic bikes differently in order to design effective marketing strategies that convert casual riders to annual memberships.

## **Recommendations**
* We can introduce a new pass like **weekend pass** for casual riders as they are using the bikes mostly only during the weekends .
* Implement a **Seasonal Pass** for casual riders , so they will buy the pass during the summer , as their ride count increased during hotter months of the year. This pass may encourage more people to buy the seasonal pass.
* Do lot of **promotions and membership deals** where casual riders’ popular stations and encourage them to use weekend pass and seasonal pass for more benefits .
* Offer **Discounts and create new membership deals** which will be beneficial for casual riders , also getting a Survey from them will make a better understanding of them . This maybe helpful in converting the casual riders to members.
* Giving discounts or some special deals in the membership for regular casual riders would encourage them to try casual to membership option.
* Implementing **new membership plan** for the most popular casual riders route , will be beneficial for the riders who are using that route mostly.

  
Converting casual riders to annual members will not be an easy task. But fortunately, we have meaningful and actionable insights that can help support our decision-making process.

Thank you
