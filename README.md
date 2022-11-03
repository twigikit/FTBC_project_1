# Australian Household Consumption and Expenditure Pattern: A study from 2012 - 2022
Prepared by Emma H, Kit N, Md Muhasenul H <br> *7 November 2022*
 

## Introduction
This study seeks to uncover the Australian Household consumption and expenditure pattern. Specifically, we examine:
* Where do Australian spend their money?
* How has the consumption pattern changed over the period from January 2012 to June 2022?
* Is there any relationship between key economic indicators such as unemployment and household saving, and household consumption?
* Is there any relationship between ASX 200 price movements and household consumption? <br>

We also explore if there is any possbile Covid pandemic stimulated changes in consumption pattern. Care should be taken when interpreting the time series analysis results. 


## Data Used
The following data has been used in the study:
* Australian household final consumption and expenditure quarterly seasonally adjusted chain volume measures published by the Australian Bureau of Statistics (ABS)
* Australia monthly seaosonally adjusted unemployment rate published by the ABS
* Australia quarterly seasonally adjusted household saving ratio published by the ABS
* Australia Stock Market Index data collected using the Yahoo Finance API.


### Data Cleaning and Exploration
* Economic related data were sourced from ABS, mainly using panda's read_csv method for consistency. Open API yFinance, which extracted ASX data from Yahoo Finance. Date column is set as index for further concatenation and comparison.

* We first examine the quality of each datasets by checking if there is any missing, null or duplicated value, using the ".isnull.sum()", ".duplicated()" and ".info" method, the result is none, so we conclude the dataset is clean and ready for use.

* The datasets comes in different frequency, some are daily, some are quarterly,  we used parameters, such as "index_col, "dayfirst", "parse_dates" and "infer_datetime_format, " to allow our data frames share consistent date format, and use the method of  ".plot" to visualise trend across the same timeframe of 10 years.

* In the unemployment dataset, basic statistic is run to see how the numbers are distributed, by methods of ".describe", ".max" , "idxmax" and the vice versa 'min', and 'idxmin'. We also use method of ".hvplot", and ""groupby(df.index.year).means()",  to see if particular states are more representative than the other, we decided to use the national data as they share similar pattern.

* When exploring the datasets of household saving and spending, we use method of "pct_change()" to measure its velocity of change over time, and use methods of ".concat() ", ".corr" and "seaborn.heatmap" to visualise correlation among each factors. We observed change of cash rates and household saving only has weak negative coefficient (i.e. -0.18), however rate of unemployment change are strongly corelated to household saving rate change (i.e. +0.76).

* Household spending data are extracted based on chain volume measure to remove the impact of price volatility of consumer goods, we used methods of ".groupby(df.index.year).means() " and ".plot" to visualised the trend of annualised average spending.

* We then converted the annualised averaged into percentage of spending among all the category by combining the transform method and anonymous function (i.e. "transform(lambda x: round(100 * x / df_mean.sum(axis = 1),2))", the converted result was visualised in pie chart used methods of ".subplots".


### Key observations and findings
#### Where do Australian spend their money?

<img src="./Diagram/spending_by_cat.jpg" width = "500"> <br>
In 2022, the top 5 category that Australians spend on are: <br>
* Rent
* Recreation
* Food
* Insurance
* Health

#### How has the consumption pattern changed over time?
![](./Diagram/spendingtrend.jpg)

* We observe year on year increase in household consumption and expenditure from 2012 - 2018.
* The increase in household spending seem to be plateauing between 2018 and 2019.
* As the Covid pandemic hits (late Q1 2020), we observe a significant drop in the household expenditure. This is likely driven by the mandatory lockdown and travel restrictions imposed across all states. 
* As we emerge out from pandemic, we see a steep increase in household spending.


The following barplot shows the ten year trend for each spending category.
![](./Diagram/barplot_with_popup.jpg)


#### Relationship between unemployment and household consumption
<img src="./Diagram/unemploy_corr.jpg" width="400">

**Hypothesis:** As unemployment increases, spending on discretionary items are expected to decrease; spending on necessacity are likely to remain unchanged.

**Conclusion:** The calculated correlation coefficients between unemployment and spending in each category largely agree with the hypothesis. We observed that spending on tobacco and alcohol tend to increase when unemployment increase. 

#### Relationship between household saving and household consumption
<img src="./Diagram/saving_corr.jpg" width="400">

**Hypothesis:** As unemployment increases, spending on discretionary items are expected to decrease; spending on necessacity are likely to remain unchanged.

**Conclusion:** The calculated correlation coefficients between unemployment and spending in each category largely agree with the hypothesis. We observed that spending on tobacco and alcohol tend to increase when unemployment increase. 

4. Saving is positively correlated with alcohol spending (0.766694) and negatively correlated with operation_vehicle (0.873177, recreation 0.791215, hotel 0.799859. 


#### Relationship between ASX 200 and household consumption
<img src="./Diagram/ASX_corr.jpg" width="400">


### Possible use of Data 
Looking at the changes in data we can come up with a possible assumption that people are travelling less due to work from home arrangement. 

Spending in telecommunicaiton has increased due to advance work from home set up is causing people to spend more on telecoomunication for connectivity from home. 

Pople are more health concern since there is a significant drop in tobaco consumption and additional spending on health. 

If any business wants to invest their money they can work on investing in telecommunication, health related products. 

Car importers may need to think differently for introducing vehicles supporting recreation more than day to day transport. 


### Future Development

What are the ares of telecoomunication people are spending and whether there is any scope of fintech companies to play role in that areas. 

### References

https://pypi.org/project/yfinance/

