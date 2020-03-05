# San_Francisco_BikeShare_Analysis
Analysis of the effects of weather on the riding habits of people in San Francisco, based on the public data of the Bay Wheels bikesharing program.

This is based on : 

Official weather data from the NOAA : https://www.ncdc.noaa.gov/data-access/land-based-station-data

As well as : 

Bay Wheels data for 2017 to 2018 : https://www.lyft.com/bikes/bay-wheels/system-data

# Conclusion : 

### Exploration :

- We found that the the number of bikes in the program increased from ~500 to ~3000 during the year June 2017 to June 2018 of the San Francisco Bay wheels sharing progam.
- We also found that the total number of trips done per month in the network increased over this period. We put into light the fact that the number of rides at the beginning of the bikesharing service was low during the time it took for the service to gain traction among its customers.
- We found, surprisingly, that a bike was only used on average 2 times a day during the week and 1.5 times a day on the weekend, suggesting that the network is very heavily underused.
- We tried looking if the usage patterns of bikes was different on public holidays, but the number of public holidays in San Francisco was too small to discover a trend.
- Despite the fact that 95% of trips are below 40 minutes, the remaining 5% outliers skewed heavily the average trip duration, and we decided to remove the outliers from the dataset to be able to build models on the effect of temperature and precipitation on the average trip duration.
- There was a very large difference in the usage patterns of bikes during the days from Monday to Friday and during the weekend. The bike use during the week is bimodal, corresponding to a usage peak in the morning when people go to work (around 8 am) and in the afternoon, when they come back (around 5/6 pm). The bike use during the weekend is more uniformly distributed throughout the days. We also found that there were less trips per day during the weekend than during the business days and also that trips lasted longer on average during the weekends (13.8 versus 10.7 minutes when we remove the outliers)
- The overwhelming majority of rides were done by subscribers, and subscribers tended to do shorter trips than customers, and customers had a usage pattern that was less marked by commuting peaks.

### Model building :

- We built a model for the distribution of trip durations, by fitting a beta distribution, which depends on the weekend/business day split, we could use such a distribution to solve the problem of predicting when stations will become empty.

- We also managed to find a way to estimate the virtual number of trips that the bikesharing program would have had in the beginning months, had it been already adopted by many customers. We could have done that by simply taking future data, but it was an interesting challenge to try to use another bikesharing program to estimate these values, as we would have had to do, had we been in the shoes of a Bay Wheels data scientist in 2018. We did so by looking at the data of another bikesharing program through a public Kaggle dataset.

- We also built a model that estimated the impact of precipitation and temperature on the number and duration of trips, and the results seem consistent : when we control for month, usertype, hour, and weekend, Precipitation tends to reduce the number and duration of trips whereas Temperature tends to increase both.
