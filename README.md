# Conversion-Rate


![alt text](https://github.com/PINGGEZI/Conversion-Rate/blob/main/WX20220601-122932%402x.png)

## Goal

Optimizing the conversion rate is very important for business. It helps the business to grow their customer base, reduces the cost of advertising cacampaigns and as a result, generates more revenue. 

This project aims to predict the conversion rate by building a model, find out what kind of features have an impact on the conversion rate,and which segments perform good or bad. Based on the findings, I will provide insights for the marketing team. 

The data contains the demographic charateristics (eg: sex,age) and the browsing behaviours of the users. A user was considered "Converted" if end up buying something within a session, and vice versa. 

## About Data

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

### Data Descriptions
Before deep dive into the data, let's take a look at the descriptive statistics of the data and get a basic understanding of it. 

<br>

<img width="582" alt="image" src="https://user-images.githubusercontent.com/47039591/173699709-ca204dd3-4fc7-49e0-a723-e376a7a73598.png">

A Few Quick Observations:
* The data set contains 316200 observations with no missing values.

* The conversion rate at ~3% is industry standard, which makes sense. 


* The user base is quite young with average age of 30.


* More than half of the users clcking the site have an account alreday. 

* Maximum age of 123 looks suspicious!! After examination, I found that two users reported themselves as older than 110-year-old. These records are not so reliable, so just remove these rows.

### Key Findings
**(1)**

<img width="674" alt="image" src="https://user-images.githubusercontent.com/47039591/173702375-210efe26-df26-4cd4-8556-d6a311f6ece8.png">

 * No doubt old users converted at a much higher rate than new users.

 * New users performed nearly identically across channels. Which means, users barely made an purchase at the time they created an account regardless how they came to the site.

 * Interestingly, old users coming to the site by directly typing the URL typically had stronger purpose, but they converted at a lower rate than those attracted by ads 'at random'. Did the ads provide good offer or did the ads effectively promote the features of the product? 

**(2)**

<img width="673" alt="image" src="https://user-images.githubusercontent.com/47039591/173702449-16a664a6-292c-424a-8d59-55b08d3bcbf3.png">

* The users came from 4 different countries, mainly the US. This website is probably a US website.

* The plot shows that Germany has the highest conversion rate ~6% among all even though it has the least number of users. Then the UK comes after with ~5%. China, however, has extremely low conversion rate far less than 1%, which is abnormal.

**(3)**

<img width="580" alt="image" src="https://user-images.githubusercontent.com/47039591/173702548-70f54aea-99d7-4e49-8d87-95a684d3151b.png">
As we can see, only ~3.2% users converted. The data is extremely imbalanced. 

