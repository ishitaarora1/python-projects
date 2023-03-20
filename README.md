# **Introduction to the case study**


In 2016, Cyclistic launched a successful bike-share offering. Since then, the program has grown to a fleet of 5,824 bicycles that
are geotracked and locked into a network of 692 stations across Chicago. The bikes can be unlocked from one station and
returned to any other station in the system anytime.
Until now, Cyclistic’s marketing strategy relied on building general awareness and appealing to broad consumer segments.
One approach that helped make these things possible was the flexibility of its pricing plans: single-ride passes, full-day passes,
and annual memberships. Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers
who purchase annual memberships are Cyclistic members.
Cyclistic’s finance analysts have concluded that annual members are much more profitable than casual riders. Although the
pricing flexibility helps Cyclistic attract more customers, Moreno believes that maximizing the number of annual members will
be key to future growth. Rather than creating a marketing campaign that targets all-new customers, Moreno believes there is a
very good chance to convert casual riders into members. She notes that casual riders are already aware of the Cyclistic
program and have chosen Cyclistic for their mobility needs.
Moreno has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to
do that, however, the marketing analyst team needs to better understand how annual members and casual riders differ.

# **Buiseness Task**

To analyse the latest 12 months of cyclistic  bike share trips data ,  to understand the difference between the casual riders and annual members , and eventually design effective marketing strategies  to convert casual riders into annual members ,so as to increase the profit of the company.

# **Data Source**
​
the Cyclistic's historical trip data , has been made available on kaggle.com , as public dataset  by
Motivate International Inc under this license. https://ride.divvybikes.com/data-license-agreement

# **Importing the required libraries**

import pandas as pd

from pandas.api.types import CategoricalDtype

import seaborn as sns

import matplotlib.pyplot as plt

%matplotlib inline

import numpy as np


# **Uploading the 12 months datasets**

df1 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_jan_2022.csv',parse_dates=['started_at','ended_at'])

df2= pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_feb_2022.csv',parse_dates=['started_at','ended_at'])

df3 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_march_2022.csv',parse_dates=['started_at','ended_at']) 

df4 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_april_2022.csv',parse_dates=['started_at','ended_at'])

df5 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_may_2022.csv',parse_dates=['started_at','ended_at']) 

df6 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_june_2022.csv',parse_dates=['started_at','ended_at'])

df7 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_july_2022.csv',parse_dates=['started_at','ended_at'])

df8= pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_august_2022.csv',parse_dates=['started_at','ended_at'])

df9 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_september_2022.csv',parse_dates=['started_at','ended_at']) 

df10 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_october_2022.csv',parse_dates=['started_at','ended_at'])

df11 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_november_2022.csv',parse_dates=['started_at','ended_at'])

df12 = pd.read_csv('C:\\Users\\arora\\OneDrive\\Desktop\\cyclistic files\\cyclistic_data_december_2022.csv',parse_dates=['started_at','ended_at'])

# **Combining all the data into a single dataset**

df=pd.concat([df1,df2,df3,df4,df5,df6,df7,df8,df9,df10,df11,df12],ignore_index=True)
df

# **Exploring the dataset:**


df.shape

#5667717 rows , 13 columns)


df.info(memory_usage='deep')
#1.5 GB dataframe

df.dtypes
#the columns-'started_at' and 'ended_at' column has been already converted to pandas'  'datetime64' format, to work with.

df.columns


# **Cleaning the Dataset**

#now , we will drop the columns which are not relevant to the analysis
df=df.drop(columns=['start_station_name', 'start_station_id', 'end_station_name',
       'end_station_id', 'start_lat', 'start_lng', 'end_lat', 'end_lng'])
       
       df
# we have only the relevant columns left now.

#we will create a column called 'ride_length' which contains the duration between start time and end time
df['ride_length']=(df['ended_at']-df['started_at'])/pd.Timedelta(minutes=1)

df

#we can see some negative values in the column 'ride_length' which means that the end timing is 
# less than the start timing and also , some values are 0 ,which is logically inaccurate. so, let's drop them.


neg_row= df[df['ride_length']<1].index
# shows the index of all such negative value rows


#to drop them

df=df.drop(neg_row)

#drops all values less than 1


df=df.reset_index().drop(columns='index')          

#resetting the index and dropping the index of the old dataframe 

#now , the dataframe containing the values less than 1 is empty , this means all irrelevant values have been dropped.
df[df['ride_length']<1]


let's check how many rows we are left with !
df.shape

# there are around 21 lakh rows left out of around 22 lakh rows earlier , approximately , 5.67% of rows are deleted .


# now , let's check for any null or duplicate values
df.isnull().sum().sum()


df.duplicated().sum()

#there are no null and duplicate values .


# **Now , let's add some more relevant columns before we begin our analysis**

# **Preparing for Analysis**

 #adding the month column
df['month']=df['ended_at'].dt.month_name()

#adding the hour column
df['hour']=df['started_at'].dt.hour

#adding the year column
df['year']=df['started_at'].dt.year

#adding the weekday column
df['day_of_Week']=df['started_at'].dt.day_name()


# **Documentation of all the changes done to the data**

1) changed the format of the columns 'started_at' and 'ended_at' to pandas' 'datetime64[ns]' format.

2) deleted the columns 'start_station_name', 'start_station_id', 'end_station_name',
       'end_station_id', 'start_lat', 'start_lng', 'end_lat', 'end_lng'.
       
3) created the column 'ride_length' from (('ended_at'- 'started_at) , which contained the trip duration of each rider .

4) deleted all the rows where the 'ride_length' column had value <1

5) extracted the year from the 'started_at' column to make a new column containing 'year of ride'.   

6) extracted the month name  from the 'started_at' column to make a new column containing month of ride.  

7) extracted the weekday from the 'started_at' column to make a new column containing day of week of the ride

8) extracted the hour from the 'started_at' column to make a new column containing hour of the ride     


# **Analysis of Data**

#most popular day of week to cycle
df.groupby("member_casual")['day_of_Week'].describe()

#saturday is the most popular day of week for both members and casuals.


#most popular month to cycle
df.groupby("member_casual")['month'].describe()

# june is the most popular month for both members and casuals.


# average ride_length for members and casual riders by day of week
order_of_days=['Monday', 'Tuesday','Wednesday','Thursday','Friday','Saturday','Sunday']

avg_ride_length =df.groupby(['member_casual','day_of_Week'])['ride_length'].mean()

#setting the correct order
pd.DataFrame(avg_ride_length).reindex(index=order_of_days,level=1)








