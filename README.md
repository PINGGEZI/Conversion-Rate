# Conversion-Rate


![alt text](https://github.com/PINGGEZI/Conversion-Rate/blob/main/WX20220601-122932%402x.png)

## Goal

Optimizing the conversion rate is very important for business. It helps the business to grow their customer base, reduces the cost of advertising cacampaigns and as a result, generates more revenue. 

This project aims to predict the conversion rate by building a model, find out what kind of features have an impact on the conversion rate,and which segments perform good or bad. Based on the findings, I will provide insights for the marketing team. 

The data contains the demographic charateristics (eg: sex,age) and the browsing behaviours of the users. A user was considered "Converted" if end up buying something within a session, and vice versa. 

## Data Descriptions

The dataset contains 316,200 observations. Each rows represents a unique user with his/her own features. **Converted** feature is our target variable, taking value 1 (converted) or 0 (not converted)

* **country** : user country based on the IP address

* **age** : user age. Self-reported at sign-up step

* **new_user** : whether the user created the account during this session or had already an account and simply came back to the site

* **source** : marketing channel source
  * **Ads**: came to the site by clicking on an advertisement
  * **Seo**: came to the site by clicking on search results
  * **Direct**: came to the site by directly typing the URL on the browser

* **total_pages_visited**: number of total pages visited during the session. This can be seen as a proxy for time spent on site and engagement

* **converted**: this is our label. 1 means they converted within the session, 0 means they left without buying anything. The company goal is to increase conversion rate: # conversions / total sessions


## Exploratory Data Analysis

* The data set contains 316200 observations with no missing values.

* The conversion rate at ~3% is industry standard, which makes sense. 


* The user base is quite young with average age of 30.


* More than half of the users clcking the site have an account alreday. 

* Maximum age of 123 looks suspicious!! Let's look closer.



