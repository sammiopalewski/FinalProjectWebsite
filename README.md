# [Fin 377 Final Project](https://sammiopalewski.github.io/FinalProjectWebsite/)

This is a website to showcase our final project for FIN 377 - Data Science for Finance course at Lehigh University.

To see the complete analysis file(s) click [here](https://github.com/julioveracruz/testwebsite/blob/main/notebooks/example.ipynb).


## Table of contents
1. [Introduction](#introduction)
2. [Methodology](#meth)
3. [Section 2](#section2)
    1. [Subsection](#subsec2-1)
    2. [Subsection](#subsec2-2)
4. [Analysis Section](#section3)
5. [Summary](#summary)

## Introduction  <a name="introduction"></a>

(The "Introduction" text above is formatted in heading 2 style.) The main goal of this project is to explore the relationship between subscriber count of streaming services and stock returns of subsidiary companies. We will also be looking at how specific events impacted the stock returns and subscriber counts in a dashboard linked [here](https://finalproject-bt8gkfbzkptf7gkk8yhyka.streamlit.app/).   

## Methodology <a name="meth"></a>

Here is some code that we used to develop our analysis. This is the code we used to conduct our regression analysis between subscriber count and stock returns for Amazon Prime and Amazon respectively. [More details are provided in the Appendix](page2).

Note that for the purposes of the website, you have to copy this code into the markdown file and  
put the code inside trip backticks with the keyword `python`.

```python
import pandas as pd
import pandas as pd
from sklearn.linear_model import LinearRegression

# Step 1: Filter dates for stock returns to specific order
filtered_returns_df_disney = disney_data_ret[['Date', 'Close', 'Adj Close']]

# Filter for specific dates
specific_dates = ['2019-10-01', '2020-01-02', '2020-02-01', '2020-07-01', '2020-10-01' , '2021-01-04' , '2021-04-01' , 
                  '2021-07-01' , '2021-10-01' ,'2022-01-03' , '2022-04-01' , '2022-07-01' , '2022-10-03' , '2023-01-03'
                  '2023-04-03' , '2023-07-03' , '2023-10-02' , '2024-01-02']
filtered_returns_df_disney = filtered_returns_df_disney[filtered_returns_df_disney['Date'].isin(specific_dates)]

print(filtered_returns_df_disney)

# Print the DataFrame after preprocessing
print("Preprocessed Subscriber DataFrame:")
print(disney_data_sub_reg)

#Step 3: Merge the filtered dataframe with the subscribers dataframe based on the date column
merged_df_disney = pd.merge(filtered_returns_df_disney, disney_data_sub_reg, on='Date', how='inner')
print(merged_df_disney)

disney_quarter_return = merged_df_disney['Adj Close'].pct_change() * 100

# Adding a new column titled 'quarter_return'
merged_df_disney['quarter_return'] = disney_quarter_return

# Printing the updated DataFrame
print(merged_df_disney)

import numpy as np
from sklearn.linear_model import LinearRegression

merged_df_disney.dropna(subset=['quarter_return', 'Number of Subs (mil)'], inplace=True)

# Reshape X to a 2D array
X = merged_df_disney['quarter_return'].values.reshape(-1, 1)
y = merged_df_disney['Number of Subs (mil)']

# Create and fit the model
model = LinearRegression()
model.fit(X, y)

# Get coefficients
slope = model.coef_[0]
intercept = model.intercept_

# Print results
print("Regression Equation: y = {:.2f}x + {:.2f}".format(slope, intercept))

# Calculate R-squared
r_squared = model.score(X, y)

# Print R-squared
print("R-squared:", r_squared)
```

Notice that the output does NOT show! **You have to copy in figures and tables from the notebooks.**

## Section <a name="section2"></a>
Blah blah

### Subsection 1 <a name="subsec2-1"></a>
This is a subsection, formatted in heading 3 style

### Subsection 2 <a name="subsec2-2"></a>
This is a subsection, formatted in heading 3 style

## Analysis Section <a name="section3"></a>

Here are some graphs that we created in our analysis. We saved them to the `pics/` subfolder and include them via the usual markdown syntax for pictures.

![](pics/plot1.png)
<br><br>
Some analysis here
<br><br>
![](pics/plot2.png)
<br><br>
More analysis here.
<br><br>
![](pics/plot3.png)
<br><br>
More analysis.

## Summary <a name="summary"></a>

Blah blah



## About the team
Sammi Opalewski 
<img src="" alt="" width="300"/>
Sammi is a junior majoring in Finance and minoring in Applied Mathematics. 
<br>
Chris Toh
<br>
Chris is a senior majoring in IBE Financial Engineering.
<br><br><br>
<img src="" alt="" width="300"/>
<br>
Sam Fleetwood
<br>
Sam is a senior majoring in IBE Finance and Industrial Engineering. 
<img src="" alt="" width="300"/>
<br>
Matt Slaski
<br>
Matt is a senior majoring in IBE Finance. 
<br><br><br>
<img src="" alt="" width="300"/>
<br>


## More 

To view the GitHub repo for this website, click [here](https://github.com/donbowen/teamproject).
