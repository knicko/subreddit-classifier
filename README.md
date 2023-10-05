# 1. Problem Statement:
My name is Nicholas Nguyen and I work for Reddit as a Data Scientist. We are conducting an early beta experiment for Reddit users to make posts without having to think about which subreddit to post to. We are developing a system where users can easily make a post and then be referred to which subreddit they should make the post public from!

Using Pushshift's API, collect posts from r/Cryptocurrency and r/Stocks
Use NLP to train a binary classifier on which subreddit a given post came from

# 2. Description of Data
The dataset that I used consisted of ~ 10,000 pulls of submissions split from r/CryptoCurrency & r/Stocks
The features consisted of numerous random features however, none of the matters because this is a Binary Classification problem. I only needed to train a model that predicts which subreddit the posts come from. So with that in mind, I left only 2 columns; Subreddit & Texts.

Subreddit column got dummified or encoded as binary variables.
- 0 = Cryptocurrency
- 1 = Stocks

Target: Logistic Regression, K-Nearest Neighbors Classifier, Support Vector Classifier

Data Dictionary:

| Feature | Type   | Dataset | Description  |
|---------|--------|---------|--------------|
|   Subreddit     |   boolean|    reddit pull    |  0 = Cryptocurrency, 1 = Stocks       |
|  Title     |   string|    reddit pull    |  titles of the reddit posts       |

EDA: 
1. Most common words for both subreddits using CVEC

2. Most important words for both subreddits using TVEC

![image.png](images/10_import_crypto.png)
For r/cryptocurrency, we notice that people are interested in anything that is 'new' and 'moons'. That just goes to show that most stuff in crypto are high risk and high reward opportunities. 

![image.png](images/10_import_stocks.png)
For r/stock, we notice that people are interested in anything that is 'trading' and 'help'. This shows that r/Stocks users are more inclined to "trading" stocks. That means making several trades a day. And 'help' could mean lots of people ask for help in this subreddit.

There are 2 main functions that were used in this project. 

Reddit:
a function used to pull the subreddit information using pushshift.io API. This function inputs a which subreddit you want to pull from, the size of your pull, and how many pulls to execute. Then returns the full concatenated dataframe involving number of pulls and sizes.

Input_Model:
a function used to fit a pipeline with multiple models using Count Vectorizer and TFIDF Vectorizer. This function inputs a dataframe, and which model you want to run. Then returning the best gridsearch parameters, training and testing scores for CVEC and TVEC, specificity and accuracy scores, and a confusion matrix.

# 3. I fitted 3 models

The accuracy metric was the most important metric used for determining which model performed the best.

## K-Nearest Neighbors
Count Vectorizer:
Training score: 0.8278
Test score: 0.7270
Accuracy: 0.7270

Tfidf Vectorizer (highly overfit):
Training score: 0.9530
Test score: 0.5844
Accuracy: 0.5844

## Logistic Regression
Count Vectorizer:
Training score: 0.9588
Test score: 0.9010
Accuracy: 0.9010

Tfidf Vectorizer:
Training score: 0.9530
Test score: 0.9014
Accuracy: 0.9014

## Support Vector Classifier
Count Vectorizer:
Training score: 0.9522
Test score: 0.8877
Accuracy: 0.8877

Tfidf Vectorizer:
Training score: 0.9910
Test score: 0.9048
Accuracy: 0.9048 (highest)

# 4. Conclusion
In conclusion, we found that the Tfidf fitted Support Vector Classifier was the model that performed the best. We used the accuracy metric. This can help users by recommending which post is to be more fit in a specific subreddit. A good way to build upon this would be to create a system that can take in the top 2 subreddits in each category of reddit, then run the SVC model to recommend users which subreddit their post should lead to. For example, this model can be used for subreddits r/PS4 and r/XBOX. This would clearly identify if a users should be posting in the xbox subreddit or ps4. An addition is if a user wants more upvotes, we can sort by which words contain posts with the most upvotes. More useful data that should be collected is upvotes and downvotes. Perhaps a percentage can be made for those with specific words. So my conclusion is that is the very core model that can be highly built upon. More variables can be added to produce better recommendations. 