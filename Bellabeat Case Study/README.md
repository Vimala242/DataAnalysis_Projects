# Bellabeat Case Study
## Introduction
As a Junior Data Analyst on the Marketing Analysis team at Bellabeat, a company specializing in high-tech health products for women, I’ve been tasked with analyzing the fitness data from the Bellabeat app and smart devices. My primary focus is to understand how customers are using these devices, looking for patterns and insights that can drive the company’s marketing strategy. The findings from my analysis will be used to guide decision-making and will be presented to the executive team to help refine and enhance Bellabeat’s marketing approach.
### About the company
Bellabeat, a high-tech manufacturer of health-focused products for women. Although, a successful small company, they have the potential to become a larger player in the global smart device market.
Urška Sršen and Sando Mur founded Bellabeat. Sršen used her background as an artist to develop beautifully designed technology that informs and inspires women around the world. Since it was founded in 2013, Bellabeat has grown rapidly and quickly positioned itself as a tech-driven wellness company for women.
### Characters and products
### Characters
* **Urška Sršen:** Bellabeat’s cofounder and Chief Creative Officer.
* **Sando Mur:** Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team.
* **Bellabeat marketing analytics team:** A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy.
### Products
* **Bellabeat app:** The Bellabeat app provides users with health data related to their activity, sleep, stress,menstrual cycle, and mindfulness habits. This data can help users better understand their current habits and make healthy decisions. The Bellabeat app connects to their line of smart wellness products.
* **Leaf:** Bellabeat’s classic wellness tracker can be worn as a bracelet, necklace, or clip. The Leaf tracker connects to the Bellabeat app to track activity, sleep, and stress.
* **Time:** This wellness watch combines the timeless look of a classic timepiece with smart technology to track user activity, sleep, and stress. The Time watch connects to the Bellabeat app to provide you with insights into your daily wellness.
* **Spring:** This is a water bottle that tracks daily water intake using smart technology to ensure that you are appropriately hydrated throughout the day. The Spring bottle connects to the Bellabeat app to track your hydration levels.
## Step 1: Ask
### Business Task
  * **Objective:** Analyze Fitbit data to derive insights that can inform and shape Bellabeat's marketing strategy, with the goal of expanding its presence and establishing itself as a global leader.
  * **Key Stakeholders:**
      * **Urška Sršen** - Bellabeat’s cofounder and Chief Creative Officer
      * **Sando Mur** - Bellabeat’s cofounder; key member of the Bellabeat executive team
      * **Bellabeat marketing analytics team**
## Step 2: Prepare
#### Data Source:
The data for our case study comes from the Fitbit Fitness Tracker dataset, which is hosted on Kaggle and made available through Mobius.
#### Accessibility and privacy of data:
Upon reviewing the metadata of the dataset, we can confirm that it is open-source. The creator has released the work to the public domain, relinquishing all rights under copyright law globally, where permitted. This means the dataset can be copied, modified, distributed, and used for commercial purposes without needing permission.
#### Information about the dataset:
The Fitbit Fitness Tracker dataset contains personal fitness tracker from thirty fitbit users. Thirty eligible Fitbit users consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. It includes information about daily activity, steps, and heart rate that can be used to explore users’ habits.
#### Data Organization:
The dataset consists of 18 CSV files, each containing different types of quantitative data collected by Fitbit. The data is structured in a "long" format, where each row corresponds to a specific time point for an individual subject. As a result, each subject appears in multiple rows since the data is recorded by day and time. Every user is assigned a unique ID, and their data is organized based on the day and time of tracking.
#### Data Integrity and Credibility:
Given the small sample size (30 users) and the lack of demographic information, there is a potential for sampling bias. It is unclear whether the sample accurately reflects the broader population. Additionally, the dataset is not current and was collected over a relatively short two-month period, which may limit its applicability. Due to these constraints, we will approach the case study with an operational perspective, focusing on the practical insights derived from the available data.
## Step 3: Process
R Studio was chosen for this analysis due to its wide range of packages and powerful data visualization capabilities, which allowed for in-depth exploration of the data.
#### Environment Setup:
I will select the packages that are essential for my analysis and load them. The packages to be used for my analysis include:
* tidyverse
* here
* skimr
* janitor
* lubridate
#### Installing the packages:
```
install.packages("tidyverse")
install.packages("here")
install.packages("skimr")
install.packages("janitor")
install.packages("lubridate")
```
install.packages("tidyverse")

Installing package into ‘/cloud/lib/x86_64-pc-linux-gnu-library/4.4’ (as ‘lib’ is unspecified)

install.packages("here")

Installing package into ‘/cloud/lib/x86_64-pc-linux-gnu-library/4.4’ (as ‘lib’ is unspecified)

install.packages("skimr")

Installing package into ‘/cloud/lib/x86_64-pc-linux-gnu-library/4.4’ (as ‘lib’ is unspecified)

install.packages("janitor")

Installing package into ‘/cloud/lib/x86_64-pc-linux-gnu-library/4.4’ (as ‘lib’ is unspecified)

install.packages("lubridate")

Installing package into ‘/cloud/lib/x86_64-pc-linux-gnu-library/4.4’ (as ‘lib’ is unspecified)
#### Loading the libraries:
```
library(tidyverse)
library(here)
library(skimr)
library(janitor)
library(lubridate)
```
![Loading_Libraries](https://github.com/Vimala242/DataAnalysis_Projects/tree/main/Bellabeat%20Case%20Study/load_libraries.jpg)
#### Importing data files:
The CSV files were initially opened in Excel, where the time and/or date formatting was adjusted from "custom" to "time" and/or "short date" as needed. Afterward, the files were imported into R Studio, and data frames were created with simplified names for easier reference.
```
daily_activity <- read.csv("/kaggle/input/fitbit/Fitabase Data 4.12.16-5.12.16/dailyActivity_merged.csv", header = TRUE)
daily_steps <- read.csv("/kaggle/input/fitbit/Fitabase Data 4.12.16-5.12.16/dailySteps_merged.csv", header = TRUE)
daily_sleep <- read.csv("/kaggle/input/fitbit/Fitabase Data 4.12.16-5.12.16/sleepDay_merged.csv", header = TRUE)
hourly_steps <- read.csv("/kaggle/input/fitbit/Fitabase Data 4.12.16-5.12.16/hourlySteps_merged.csv", header = TRUE)
hourly_calories <- read.csv("/kaggle/input/fitbit/Fitabase Data 4.12.16-5.12.16/hourlyCalories_merged.csv", header = TRUE)
hourly_intensities <- read.csv("/kaggle/input/fitbit/Fitabase Data 4.12.16-5.12.16/hourlyIntensities_merged.csv", header = TRUE)
weight <- read.csv("/kaggle/input/fitbit/Fitabase Data 4.12.16-5.12.16/weightLogInfo_merged.csv", header = TRUE)
```
#### Validating data,
```
head(daily_activity)
head(daily_sleep)
head(daily_steps)
head(hourly_calories)
head(hourly_intensities)
head(hourly_steps)
head(weight)
```
#### Check the structure of the data sets using str()
I will check the summary of the selected data frames.
```
str(daily_activity)
str(daily_sleep)
str(daily_steps)
str(hourly_calories)
str(hourly_intensities)
str(hourly_steps)
str(weight)
```
#### Cleaning and formating
Now that I know more about the structure of the data. I will check for inconsistencies and errors.

#### Check the number of participants for each data set
I will make sure to check the number of unique users per data frame before coming on with the cleaning process.
```
n_unique(daily_activity$Id)
n_unique(daily_sleep$Id)
n_unique(daily_steps$Id)
n_unique(hourly_calories$Id)
n_unique(hourly_intensities$Id)
n_unique(hourly_steps$Id)
n_unique(weight$Id)
```
All data sets have 33 participants each except the daily_sleep and weight data set which has 24 and 8 participants respectively.
I will drop the weight data set because 8 participants is too small a sample to draw conclusions and make recommendations.
#### Check for duplicates
I will check for any duplicates in the data
```
sum(duplicated(daily_activity))
sum(duplicated(daily_sleep))
sum(duplicated(daily_steps))
sum(duplicated(hourly_calories))
sum(duplicated(hourly_intensities))
sum(duplicated(hourly_steps))
```
#### Remove all duplicates and missing values
I will remove all duplicates and missing values from my data.
```
daily_activity <- daily_activity %>%
  distinct() %>%
  drop_na()
daily_sleep <- daily_sleep %>%
  distinct() %>%
  drop_na()
daily_steps <- daily_steps %>%
  distinct() %>%
  drop_na()
hourly_calories <- hourly_calories %>%
  distinct() %>%
  drop_na()
hourly_intensities <- hourly_intensities %>%
  distinct() %>%
  drop_na()
hourly_steps <- hourly_steps %>%
  distinct() %>%
  drop_na()
```
I will verify that duplicates has been removed.
```
sum(duplicated(daily_sleep))
```
#### Clean and rename columns
I will ensure that column names are in the right syntax and same format in all datasets since datasets will be merged later on.I will are change all columns to lower case format.
```
clean_names(daily_activity)
daily_activity <- rename_with(daily_activity, tolower)
clean_names(daily_sleep)
daily_sleep <- rename_with(daily_sleep, tolower)
clean_names(daily_steps)
daily_steps <- rename_with(daily_steps, tolower)
clean_names(hourly_calories)
hourly_calories <- rename_with(hourly_calories, tolower)
clean_names(hourly_intensities)
hourly_intensities <- rename_with(hourly_intensities, tolower)
clean_names(hourly_steps)
hourly_steps <- rename_with(hourly_steps, tolower)
```
I will check the data again to verify that changes has been effected.
```
head(daily_activity)
head(daily_sleep)
head(daily_steps)
head(hourly_calories)
head(hourly_intensities)
head(hourly_steps)
```
#### Make date and time columns consistent
I will clean date-time format for daily_activity and daily_sleep since I will merge both data frames.Note that we can disregard the time on daily_sleep data frame we are using as_date instead as as_datetime.
For our hourly_calories, hourly_intensities and hourly_steps dataset, I will convert date string to date-time.
```
daily_activity <- daily_activity %>%
  rename(date = activitydate) %>%
  mutate(date = as_date(date, format = "%m/%d/%Y"))
daily_sleep <- daily_sleep %>%
  rename(date = sleepday) %>%
  mutate(date = as_date(date, format ="%m/%d/%Y %I:%M:%S %p", tz = Sys.timezone()))
hourly_calories <- hourly_calories %>% 
  rename(date_time = activityhour) %>% 
  mutate(date_time = as.POSIXct(date_time, format ="%m/%d/%Y %I:%M:%S %p" , tz=Sys.timezone()))
hourly_intensities <- hourly_intensities %>% 
  rename(date_time = activityhour) %>% 
  mutate(date_time = as.POSIXct(date_time, format ="%m/%d/%Y %I:%M:%S %p" , tz=Sys.timezone()))
hourly_steps<- hourly_steps %>% 
  rename(date_time = activityhour) %>% 
  mutate(date_time = as.POSIXct(date_time, format ="%m/%d/%Y %I:%M:%S %p" , tz=Sys.timezone()))
```
#### Merging data sets
I will merge the daily_activity and daily_sleep data sets together.
```
daily_activity_sleep <- merge(daily_activity, daily_sleep, by=c ("id", "date"))
```
I will take a look at the merged datasets.
```
glimpse(daily_activity_sleep)
```
## Steps 4 & 5: Analyze and Share
I will analyze trends of the users of FitBit and determine if that can help me on BellaBeat's marketing strategy.

#### Summarize and explore each data set
#### daily_activity summary,
```
daily_activity %>%  
  select(totalsteps,
         totaldistance,
         sedentaryminutes, calories) %>%
  summary()
```
#### Exploring number of active minutes per category,
```
daily_activity %>%
  select(veryactiveminutes,
         fairlyactiveminutes,
         lightlyactiveminutes) %>%
  summary()
```
#### daily_sleep data summary,
```
daily_sleep %>%
  select(totalsleeprecords,
         totalminutesasleep,
         totaltimeinbed) %>%
  summary()
```
#### hourly_calories data summary
```
hourly_calories %>%
  select(calories) %>%
  summary()
```
### Discoveries from the summary
* Average total steps is 7638 in a day. The daily recommended amount of steps to be taken per day is 7500
* Sedentary minutes on a average is 991(~17 hours). This needs to be reduced.
* Majority of the participants are light users.
* Participants sleep for an average of 419 minutes (~7 hours).
* A total of 97 calories is burned per hour on a average.

#### Steps taken and Calories burned
I will make a visualization to check if there's a correlation between steps taken and the amount of calories burned.
```
ggplot(data = daily_activity, aes(x = totalsteps, y = calories)) + 
  geom_point() + geom_smooth() + labs(title ="Total Steps vs. Calories")
```

I see a positive correlation between total steps taken and the amount of calories burned.​
#### Steps per weekday
To know what day of the week users are more active.
```
weekday_steps <- daily_activity %>%
  mutate(weekday = weekdays(date))
weekday_steps$weekday <-ordered(weekday_steps$weekday, levels=c("Monday", "Tuesday", "Wednesday", "Thursday",
                                                                "Friday", "Saturday", "Sunday"))
weekday_steps <-weekday_steps %>%
  group_by(weekday) %>%
  summarize (daily_steps = mean(totalsteps))

head(weekday_steps)
```
Now that we have gotten the steps taken for each day of the week.I will make a visualization to better understand the data.
```
ggplot(weekday_steps, aes(weekday, daily_steps)) +
  geom_col(fill = "#d62d58") +
  geom_hline(yintercept = 7500) +
  labs(title = "Daily steps per weekday", x= "", y = "") +
  theme(axis.text.x = element_text(angle = 45,vjust = 0.5, hjust = 1))
```
#### Sleep per weekday
To know what day of the week users sleep the most.
```
weekday_sleep <- daily_sleep %>%
  mutate(weekday = weekdays(date))
weekday_sleep$weekday <-ordered(weekday_sleep$weekday, levels=c("Monday", "Tuesday", "Wednesday", "Thursday",
                                                                "Friday", "Saturday", "Sunday"))

weekday_sleep <-weekday_sleep %>%
  group_by(weekday) %>%
  summarize (daily_sleep = mean(totalminutesasleep))

head(weekday_sleep)
```
#### Make a visualization,
```
ggplot(weekday_sleep, aes(weekday, daily_sleep)) +
  geom_col(fill = "#db7992") +
  geom_hline(yintercept = 480) +
  labs(title = "Minutes asleep per weekday", x= "", y = "") +
  theme(axis.text.x = element_text(angle = 45,vjust = 0.5, hjust = 1))
```
## Discoveries from the above analysis
* In the graphs above we can deduce that users don't take the recommended amount of sleep of 8 hours.
* Users take recommended number of 7500 steps a day excepts for Sundays.
#### Hourly intensities throughout the day
​Split the datetime column into date and time columns.
```
hourly_intensities <- hourly_intensities %>%
  separate(date_time, into = c("date", "time"), sep= " ") 

head(hourly_intensities)

hourly_intensities <- hourly_intensities %>%
  group_by(time) %>%
  drop_na() %>%
  summarise(mean_total_int = mean(totalintensity))
```
I will make a visualization of the hourly intensities data.
```
ggplot(data = hourly_intensities, aes(x = time, y = mean_total_int)) + geom_histogram(stat = "identity", fill='purple') +
  theme(axis.text.x = element_text(angle = 90)) +
  labs(title="Average Total Intensity vs. Time")
```
## Discoveries after analyzing intensities(hourly)
* I found out that people are more active between 5am and 10pm.
* Most of the activity happens between 5 pm and 7 pm - I suppose that when people are done with work for the day, they go to the gym or take a walk.We can use this period of time to remind and motivate users to go for a run or walk using the Bellabeat app.
#### Hourly steps throughout the day
Separating the datetime column into date and time column.
```
hourly_steps <- hourly_steps %>%
  separate(date_time, into = c("date", "time"), sep= " ") %>%
  mutate(date = ymd(date)) 

head(hourly_steps)
```
I will make a visualization of the hourly steps throughout the day.
```
hourly_steps %>%
  group_by(time) %>%
  summarize(average_steps = mean(steptotal)) %>%
  ggplot() +
  geom_col(mapping = aes(x=time, y = average_steps, fill = average_steps)) + 
  labs(title = "Hourly steps throughout the day", x="", y="") + 
  scale_fill_gradient(low = "red", high = "green")+
  theme(axis.text.x = element_text(angle = 90))
```
#### Discoveries
* Users are more active from 8am to 5pm and they walk more steps from 12pm to 2pm and 5pm to 7pm.
* I assume that most users are working class women and the time more steps are recorded suggests that they have their lunch break (12pm-2pm) and close for the day (5pm-7pm) during those period.
#### Type of user based on the number of days smart device was used
Calculate the number of users that use their smart device on a daily basis, classifying our sample into three categories knowing that the duration of the survey is 31 days:
* High user - users who use their device for 21-31 days
* Moderate user - users who use their device for 10-20 days
* Low user - users who use their device for 1-10 days
Next,I will create a new data frame grouping by id, calculate the number of days smart device was used and create a new column with the classification explained above.
```
daily_use <- daily_activity_sleep %>%
  group_by(id) %>%
  summarize(days_used=sum(n())) %>%
  mutate(user_type= case_when(
    days_used >= 1 & days_used <= 10 ~ "low user",
    days_used >= 11 & days_used <= 20 ~ "moderate user", 
    days_used >= 21 & days_used <= 31 ~ "high user", 
  ))

head(daily_use)
```
Create a percentage data frame to better visualize the results in the graph.
```
daily_use_percent <- daily_use %>%
  group_by(user_type) %>%
  summarise(total = n()) %>%
  mutate(totals = sum(total)) %>%
  group_by(user_type) %>%
  summarise(total_percent = total / totals) %>%
  mutate(labels = scales::percent(total_percent))

daily_use_percent$user_type <- factor(daily_use_percent$user_type, levels = c("high user", "moderate user", "low user"))

head(daily_use_percent)
```
Make a visualization of the smart device usage per user.
```
daily_use_percent %>%
  ggplot(aes(x = "",y = total_percent, fill = user_type)) +
  geom_bar(stat = "identity", width = 1)+
  coord_polar("y", start=0)+
  theme_minimal()+
  theme(axis.title.x= element_blank(),
        axis.title.y = element_blank(),
        panel.border = element_blank(), 
        panel.grid = element_blank(), 
        axis.ticks = element_blank(),
        axis.text.x = element_blank(),
        plot.title = element_text(hjust = 0.5, size=14, face = "bold")) +
  geom_text(aes(label = labels),
            position = position_stack(vjust = 0.5))+
  scale_fill_manual(values = c( "#d62d58","#db7980","#fc9fb7"),
                    labels = c("High user - 21 to 31 days",
                               "Moderate user - 11 to 20 days",
                               "Low user - 1 to 10 days"))+
  labs(title="Daily use of smart device")
```
From the above visualization we can deduce that:
* 50% of the users of our sample use their device frequently - between 21 to 31 days.
* 12% are moderate users (they use their device for 11 to 20 days).
* 38% of our sample rarely used their device.
## Step 6: Act
Bellabeat companmy was created with a mission to empower women by providing them with the data to discover more about their health and habits.
I did an analysis on the average number of steps, hours of sleep and calories burned.I also focused on the days which users are most active, the time of the day with the most activity and went further to analyze how the device was used by each user.
After analyzing the FitBit Fitness data, I will respond to the business task of helping Bellabeat on its marketing stratergy based on my results;
I would advice that for further analysis, we use tracking data from Bellabeat's device.
The datasets used have a small sample and can be biased since we didn't have any demographic details of users.
### Target audience
Our main target are young and adult women who work full-time jobs(according to hourly intensities data) and these women do some light activity to stay healthy (according to the activity type analysis). I would encourage to continue finding trends to be able to create a marketing stragety focused on them and provide knowledge about developing healthy habits.

That being said, these are my recommendations for Bellabeat company;
### Recommendation for the app
#### Daily notification on steps taken
According to CDC taking 8,000 steps per day was associated with a 51% lower risk for all-cause mortality (or death from all causes). Taking 12,000 steps per day was associated with a 65% lower risk compared with taking 4,000 steps. Bellabeat can encourage people to take at least 8 000 explaining the benefits for their health. Sending notifications daily at different times will make users conscious of the number of steps achieved so far and encourage them to meet the set target of 8000 steps according to CDC. The app can also educate users on the health benefits of walking the daily recommended number of steps.
#### Daily notification on sleep
From the results of my analysis, I can see that users have less than the recommended amount of sleep in a day. We can enable a feature on the app that allows user set up a desired time to go to sleep and receive a notification minutes before to prepare to sleep or set up an alarm to sleep.
#### Notification based on user needs
If users want to lose weight, controlling daily calorie consumption is a good idea.The Bellabeat can suggest some ideas for low-calorie food to such users.
#### Reward system
We can cvreate a reward system based on the level of activity on the app. The app could consist of stages to reach based on the amount of steps walked everyday. You need to maintain activity level for a period of time (maybe a month) to pass to the next level. For each level you would win certain amount of stars that would be converted into discount on other Bellabeat products.
#### Recommendation for the online campaign
Make sure the online campaign portrays the Bellabeat app more than just a fitness activity app. It should be seen as a guide that empowers women to strike a balance in their personal and professional life and their health habits by educating and motivating them through daily app recommendations.
