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


