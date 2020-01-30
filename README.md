# OLX- Code the Curious Challenge

## Ads Recommendation
Vedpal Rajera


The approach for the solution is as follows: 

# Preprocessing
 Reading the csv files and making data structures:
-  calculate user_count, user_ad_count and user_ad_unique.
-  Converted event time from string to pandas datetime
- calculate top 10 ads for each category which will used for new users/cold start user.
-  prepare train data based on user_data and user_message. all combination in user_message treated as true means target = 1, all combination user_data other than user_message can assume as user not interested so target = 0
- add other informarion from user data to train the model, and do data processing
- put ads information from ads table
- perform Label Encoding

# XGBoost Model Used 
Test data is prepared in way which will take care of: 
- If we have some activity of the user in that category : Content Based Recommendation. 
- Else, if we  dont have any activity of the user in that category: Popularity Based Recommendation. 

XGBoost algorithm using following features:
    'event', 'origin', 'images_count', 'ad_impressions', 'ad_views','ad_messages', 'year', 'month', 'dayofyear',
    'dayofweek', 'day','seller_id', 'price', 'source', 'enabled', 'user_count', 'usr_ad_count','usr_ad_unique_count'
    
- XGBoost provides probability of each ads in a particular category. Now groupby on category id and user id to make ad_id list and also perform to get list of probablity in descending order.
- Merge top 10 ads if list of add is less then 10.
 

## Exploratory Data Analysis (EDA): 
- EDA revealed that close to 20% users in user_messages_test have messaged an ad which they recently viewed further strengthening the intuition of using the ads already viewed. 
- User journey was observed for about many users which showed that before a user messages an ad, he always has a view event associated with it. This made way for recommending the recent ads.

## Dataset Quality: 
- Most of the latitude and longitude were very close to each other, defeating the purpose of giving them explicitly (Looks like the users have been sampled out by location). 
- No missing values were found apart from the latitude and longitude making it a good dataset. 


# Running the code
### Requirements: 
Python 3.7
Pandas 0.18.1 http://pandas.pydata.org/
Numpy 1.12.1 http://www.numpy.org/

### Running: 
1. Keep the data csv files and the python script in the same folder and change working directory to that folder. 
2. Run the OLX-Challenge.ipynb in jupyter notebook
3. Output is in ads_recommendation.csv
