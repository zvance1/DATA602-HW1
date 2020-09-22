# DATA602-HW1
DATA 602 Homework 1

# Overview and Goals
For this project, I chose to perform data analysis on a Real Estate Valuation data set. The motivation in performing linear regression on this data is to be able to predict the house price of unit area based on other features such as the house age, distance to MRT station, number of convenience stores, and location. Additionally, when we have a predicted price of unit area, we can see how the value compares to other homes with similar other features. So, if the actual price per unit area is higher than the prediction, this could potentially mean that the price per unit is too high and a real estate agent may advise a buyer to look at cheaper per unit homes that have similar features. Doing so will make buyers happier as they pay less for the similar houses giving them higher value. This leads to more buyers coming to this real estate agent and better business for them.

# How to Navigate
[Data](https://github.com/zvance1/DATA602-HW1#data) -
[Methods](https://github.com/zvance1/DATA602-HW1#methods) -
[Conclusions](https://github.com/zvance1/DATA602-HW1#conclusions) -
[Project Info](https://github.com/zvance1/DATA602-HW1#project-info) -

The data in its CSV format is located in the data directory of this repository.  Also in this data directory is the csv I wrote after cleaning the data.  In the notebooks repository you will find three jupyter notebooks - one for the loading and cleaning of the data, one for the linear regression model of the data, and lastly the technical report.  The images directory contains the visualizations used for analyzing the data.

# Data
To perform this analysis, I will use the Real estate valuation data set from the UCI Machine Learning repository. I downloaded this data as a CSV file and began the cleaning of it from there. The data contains 7 columns and 414 entires. The columns consist of the following: the transaction date, house age, distance to the nearest MRT station (in meters), number of convenience stores in the living circle on foot, geographic coordinate latitude, geographic coordinate longitude, and house price of unit area. All of these columns are of type float, except for the number of convenience stores which is an integer. A potential fall back of the data is that 414 entires is not a ton of data. Also, after removing outliers the number of entries actually used becomes 338. It is more of a challenge to represent accurate predictions for the outliers, but we leave those to be determined as that is a rare case.

# Methods
Goal: Create the best linear regression model possible to fit the data.

Techniques: 
I use pandas, seaborn, sklearn, statsmodel.api, and numpy to import, clean, and build a linear regression model on the data after importing from excel into a dataframe. The first step after reading the CSV file is to clean the data in preparation for analysis. Visualizations are created to help understand the results better.

Cleaning the data:
* Read the CSV and take a look at the data using the pandas info() and head() functions.
* The first column, No, is just an index which is not helpful so I drop it.
* Rename the columns to replace all the spaces with underscores.
* I used box and whisker plots to determine which columns needed outliers removed.  If the plot had points outside the IQR, I knew there were outliers to be removed from that column.  I calculate outliers to be outside the range of Q1 - 1.5 * IQR, and Q3 + 1.5 * IQR and return a dataframe that has them filtered out.
* When performing linear regression, one thing I found is the model performed better doing the prediction of the log of the house price of unit area than the actual value, so part of the cleaning is creating an additional column, log_house_price_of_unit_area, for which we use the numpy log function to create its values as the log of the house_price_of_unit_area column.
* Lastly, I write the cleaned pandas dataframe to a csv file to be loaded from the linear regression workbook. For the code of this cleaning, please see the load_and_clean workbook.

# Conclusions
Model results:
![regression_results.png](https://github.com/zvance1/DATA602-HW1/blob/master/images/regression_results.png)
* The R-squared is approximately 0.719 and adjusted R-squared is 0.712 (based on the number of features involved in the model). We will use the adjusted R-squared and interpret it to see that approximately 71.2% of the variation in the house price of unit area can be explained by the model. To me, this seems like a pretty decent model and about as good as we can get it.
* Looking at the next section of the results, we see that if we were to convert it to an equation, it would look like this:
predicted log_house_price_of_unit_area = -587.2630 + 0.1376 * transaction_date - 0.0083 * house_age - 0.0004 * distance_to_the_nearest_MRT_station + 0.0114 * number_of_convenience_stores + 8.5472 * latitude + 0.8298 * longitude
* Longitude is the only feature that is not significant. So, I tried removing it from the model. When removed, the R-squared drops to 0.718, and the adjusted R-squared increases to 0.713 since there is one less feature. Due to the fact that the change in effectiveness of the model is so small, I choose to leave the longitude in the model because it helps with the interpretation - both the latitude and longitude make up location and it does not make a whole lot of sense to include one and not the other.

Residual results:
![residual_results.png](https://github.com/zvance1/DATA601-HW1/blob/master/images/residual_results.png)
* Analyzing the residual plot, we can tell that we have generated a good model since there are no patterns in the residuals. They are generally random. The reason I went with the log of the house price of unit area is because when originally looking at the residual plot prior to taking the log, there was a non-constant variance of error terms - as the predicted value increased, the variance also seemed to increase.

# Project Info
<pre>
Contributors : <a href=https://github.com/zvance1>Zach Vance</a>
</pre>

<pre>
Languages    : Python3
Tools/IDE    : Anaconda, Jupyter Notebook
Libraries    : pandas, seaborn, numpy, sklearn, matplotlib, statsmodels
</pre>

<pre>
Duration     : September 2020
Last Update  : 09.22.2020
</pre>