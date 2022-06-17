# Conversion-Rate


![](https://github.com/PINGGEZI/Conversion-Rate/blob/main/WX20220601-122932%402x.png)
image source:https://capsulecrm.com/blog/improve-sales-conversion-rates/

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
 Let's take a look at the descriptive statistics of the data and get a basic understanding of it. 

<br>

<img width="582" alt="image" src="https://user-images.githubusercontent.com/47039591/173699709-ca204dd3-4fc7-49e0-a723-e376a7a73598.png">

A Few Quick Observations:
* The data set contains 316200 observations with no missing values.

* The conversion rate at ~3% is industry standard, which makes sense. 


* The user base is quite young with average age of 30.


* More than half of the users clcking the site have an account alreday. 

* Maximum age of 123 looks suspicious!! After examination, I found two users reported themselves as older than 110-year-old. These records are not so reliable, so just remove these rows.

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

## Modeling 

The Model used to predict the conversion is **Random Forest Classifer**. Remind that our target variable 'converted' is a binary, so the problem is binary classification. Here are the reasons why I picked Random Forest Classifer for our case: 

1.   Random forest is good at dealing with both discrete and continuous variables.
2.   It can identify the importance of the variables to the conversion rate.
3.   Typically, it performs very well on classification problems and prevent from overfitting with appropriate numbers of trees.

In addition, the metric I used to evaluated the model is **F1 score** since it is sensitive to imbalanced data and trades off the precision and recall. Using F1 score prevents the model bias towards the majority class to a large extent.

### Modeling Training &  Evaluation
Here the data set is splited into:

>**Training Set**: 52.5% of the data is used to train the model. \
>**Validation Set**: 22.5% of the data is used to tune the parameters. \
>**Test Set**: 25% of the data evaluate performance of the model on unseen data. 


The F1 socre on the training set is:  0.764 \
The F1 socre on the validaition set is:  0.761 \
The F1 socre on the test set is:  0.753 

<img width="1042" alt="image" src="https://user-images.githubusercontent.com/47039591/174001878-93b5edc5-5c28-4b06-928b-27aca69a23ff.png">

The model performed stably on the unseen data. The F1 score on the test set is still 0.753, is really close to the results of the training and validation set.

The Precision-Recall curve describes the trade-off between precision and recall across different thresholds, so the larger area under the curve (up to 1) the better performance of the model. The curve confirms our model performs very good too.

### Feature Importance

<img width="742" alt="image" src="https://user-images.githubusercontent.com/47039591/174201298-89a37d60-e9ac-4193-af38-7293a4cb242f.png">

* The total number of pages visited is most important according to our model.
Unfortunately, this feature is the least actionable. Because when users are ready to buy something, they typically visit more pages, such as reading the descriptions of the product, comparing prices between products. Also, purchasing a product requires users to access more pages to finish payment. \

* Source related feature seems not so important to the conversion.

### Partical Dependency Plot

<img width="949" alt="image" src="https://user-images.githubusercontent.com/47039591/174201500-70383fe3-7f72-4012-92fa-35d4b1d68178.png">

<br>

* Users with account came back to site are more likely to convert. 
* Users under 30 years old did very well. 
* UK,US and Gernmany have similar marginal impact on the conversion, with the Gernmany being the best. They all have high values, compared with China. In other words, China has very bas conversion. 
* Whichever source the users use did not matter much on the conversion.

Now, I would like to build a simple descision tree with max depth of 3 and check out which features would be most determinant when limiting the number of features.

<img width="1190" alt="image" src="https://user-images.githubusercontent.com/47039591/174202497-59f82c83-bb33-438b-ba08-f37988b70d32.png">
The simple decision tree has an agreement with the random forest on the most important segments. 

## Conclusion

* Users with old accounts do much better in terms of conversion, so targeted emails with offers or promotions to bring them back to the site could be a good strategy to try. 

* German perfroms the best among all countries. However, the total number of germany users coming to the site is the least despite a much larger population than UK. Attracting more German or improve the product awareness in German can potentially generate more values. 

* Users oder than 30 years old perfrom poorly. Does this caused by the flawless of user interface or comlexity of operations? A good actionable metric here is the conversion rate for users older than 30 years old. Is that possible to build a team foucusing on increasing this metirc? 

* Even though lots of Chinese people visited the site, the conversion rate is extremely low. There could be something wrong with the Chinese Version of the site. Does it asscoiated with poor translation, poor culture fit, or payment issues? Investigating these problems and fixing them could bring huge value to the company based on the tremendous user base in China.

