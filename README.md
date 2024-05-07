# [Fin 377 Final Project](https://sammiopalewski.github.io/FinalProjectWebsite/)

This is a website to showcase our final project for FIN 377 - Data Science for Finance course at Lehigh University.



## Table of contents
1. [Introduction](#introduction)
2. [Methodology](#meth)
4. [Analysis Section](#section3)
5. [Other Results](#summary)

## Introduction  <a name="introduction"></a>

(The "Introduction" text above is formatted in heading 2 style.) The main goal of this project is to explore the relationship between subscriber count of streaming services and stock returns of subsidiary companies. We will also be looking at how specific events impacted the stock returns and subscriber counts in a dashboard linked [here](https://finalproject-bt8gkfbzkptf7gkk8yhyka.streamlit.app/).   

## Methodology <a name="meth"></a>

Here is some code that we used to develop our analysis. This is the code we used to conduct our regression analysis between subscriber count and stock returns for Disney Disney Plus respectively. We repeated these regressions. We had to make sure that the data for subscriber count matched stock returns, so we had to claculate quarter returns and filter our stock return data to the accuarte dates. The methodology for the event analysis in found on our dashboard as well as in our report. 



```python
import pandas as pd
import numpy as np
from sklearn.linear_model import LinearRegression

# Filter dates for stock returns to specific order
filtered_returns_df_disney = disney_data_ret[['Date', 'Close', 'Adj Close']]

# Filter for specific dates
specific_dates = ['2019-10-01', '2020-01-02', '2020-02-01', '2020-07-01', '2020-10-01' , '2021-01-04' , '2021-04-01' , 
                  '2021-07-01' , '2021-10-01' ,'2022-01-03' , '2022-04-01' , '2022-07-01' , '2022-10-03' , '2023-01-03'
                  '2023-04-03' , '2023-07-03' , '2023-10-02' , '2024-01-02']
filtered_returns_df_disney = filtered_returns_df_disney[filtered_returns_df_disney['Date'].isin(specific_dates)]

print(filtered_returns_df_disney)


print("Preprocessed Subscriber DataFrame:")
print(disney_data_sub_reg)

# Merge the filtered dataframe with the subscribers dataframe based on the date column
merged_df_disney = pd.merge(filtered_returns_df_disney, disney_data_sub_reg, on='Date', how='inner')
print(merged_df_disney)

disney_quarter_return = merged_df_disney['Adj Close'].pct_change() * 100

# Adding a new column titled 'quarter_return'
merged_df_disney['quarter_return'] = disney_quarter_return


print(merged_df_disney)



merged_df_disney.dropna(subset=['quarter_return', 'Number of Subs (mil)'], inplace=True)


X = merged_df_disney['quarter_return'].values.reshape(-1, 1)
y = merged_df_disney['Number of Subs (mil)']


model = LinearRegression()
model.fit(X, y)


slope = model.coef_[0]
intercept = model.intercept_

print("Regression Equation: y = {:.2f}x + {:.2f}".format(slope, intercept))

# Calculate R-squared
r_squared = model.score(X, y)


print("R-squared:", r_squared)
```

## Analysis Section <a name="section3"></a>
The result of the regression was  y = -0.70x + 115.28 , and R^2 was 0.10155459640541864. This means that 10.16 % of the variability in stock returns explains the relationship between stock returns and subscriber counts. This R^2 is very low. Also, a negative slope means that as the stock return increased, the subscriber count decreased. As mentioned in our report, the small r^2 was not what we were expecting, and some of the other regressions had an even lower r^2. This could be do to many things. What sticks out to us is that there are many factors that can effect a company's stock, not just the increase in subscriber accounts of a owned streaming service. 

![](pics/Disney_+_Subs_Graph.png)
<br><br>
As you can see, there is a relatively constant increase in quarterly subsciber count between the years of 2020 and 2023. After that the subscriber count plateaued and stayed roughly constant. 
<br><br>
![](pics/Disney_Daily_Ret_Graph.png)
<br><br>
Here we have the daily returns of disney stock between 2000 and 2024. Through these two graphs, we can't completely tell if there is a relationship between the two, so we ran a regression model. The rest of the graphs the contain suberscriber count over time as well as stock returns over time are in the pics folder of this repo. 
<br><br>

## Other Results <a name="summary"></a>
For Amazon stock returns and Amazon Prime Subscriber count, we found R^2 to be 0.011322562195471786. 
<br>
For HBO Max subscriber counts and AT&T stock returns, we found R^2 to be 0.016821886366874983. 
<br>
For Hulu subscriber count and Disney stocks returns, we found R^2 to be 0.048301226831123034. 
<br>
For Peacock subscriber count and Comcast stock returns we found R^2 to be 0.10915861687353778.
<br>
For ESPN Plus subscriber count and Disney stock returns we found R^2 to be 0.07559649045011252.
<br>


## About the team
Sammi Opalewski 
<br>
<img src="pics/IMG_0565 (1).JPEG" alt="10" width="200"/>
<br>
Sammi is a junior majoring in Finance and minoring in Applied Mathematics. 
<br>
Chris Toh
<br>
<img src="pics/Headshot.png" alt="10" width="200"/>
<br>
Chris is a senior majoring in IBE Financial Engineering.
<br>
Sam Fleetwood
<br>
<img src="pics/LinkedInpfp.png" alt="10" width="200"/>
<br>
Sam is a senior majoring in IBE Finance and Industrial Engineering. 
<br>
Matt Slaski
<br>
<img src="pics/Professional Headshot.png" alt="10" width="200"/>
<br>
Matt is a senior majoring in IBE Finance. 

<br>


## More 

To view the GitHub repo for this website, click [here](https://github.com/sammiopalewski/FinalProjectWebsite).
<br>
To view the GitHub repo for our the final project, click [here](https://github.com/sammiopalewski/Final_Project)
<br>
To view our dashboard, click [here](https://finalproject-bt8gkfbzkptf7gkk8yhyka.streamlit.app/)
