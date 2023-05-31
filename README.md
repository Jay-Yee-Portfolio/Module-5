# Twitter Sentiment Analysis and Topic Modeling 
### Identified Multiple Users on President Trump’s Twitter  

## Abstract
It has been well documented that there are multiple users for President Trump’s twitter account based on what device a tweet was made from. The question is can we try to predict who is posting based on the contents of the tweet? That question was what sparked this project, which uses an archive of President Trump’s twitter profile now that his profile has been banned. 

## Design
After pulling tweets from a specific period (more on that later), I put the data set through EDA that included sentiment analysis in identify speech patterns. I then conducted text preprocessing and topic modeling before finally building a series of classification models.

## Data
The dataset is comprised of tweets made by President Trump (minus retweets) from June 16, 2015 through March 25, 2017. This period is from his official announcement for the presidential campaign to the day a tweet was last made from an Android device. It was known that President Trump used an Android phone up until a specific period of time, when he switched to an iPhone. The raw data includes over 5,300 tweets and several other features including the date/time the tweet was made, whether it was deleted, a retweet, or flagged. Most of the native features were dropped and additional features were added including a sentiment analysis of each tweet, counts of punctuation, and existence of URLs. 

## Algorithms
For the EDA portion, the project utilized pandas to wrangle the data while illustrating it through python’s matplotlib. Additionally, a Scattertext illustration was included to break out words for President Trump vs. his staff. Then for the NLP portion, the text was preprocessed using regex, stemming, and removal of stop words while sentiment analysis was conducted using the VADER library. 

The scattertext graph below was created to showcase the difference in wording and language used in tweets made by President Trump vs. his staff. The Android device serves as a proxy for President Trump while his staff could have made tweets from a range of other devices including iPad, iPhone, PC, etc: 
* President Trump's language was more subjective and reflective of his speaking mannerism (big, bad, media, republican, lying ted, crooked, win, bernie, badly) 
* The staff's language was more objective and reflective of instructions or updates to events (join, via, lets, support, tomorrow, American, received, see, donald, signing, live) 

![image](https://user-images.githubusercontent.com/77559909/236008046-6afa2202-fe82-47f6-b243-da36b8f605b3.png)

Futher, when these tweets were made and from what mobile device also saw a pattern. The Android user (President Trump) tweets frequently throughout the morning into late afternoon, reflecting normal working hours. The non-Android user (staff member) tweets from late afternoon through evening which could reflect any annocuements made to President Trump's followers on significant campaign events such as debates, voting deadlines, rallies, etc. Times in the graph below are based on Eastern Standard Time. 

![image](https://user-images.githubusercontent.com/77559909/236009215-343b55c3-f3ec-4a8f-89b9-0a844f2dfa41.png)

Once the EDA confirmed the possiblity of multiple users, an extensive topic modeling was conducted. Multiple doc-term matrixes using CountVectorizer and TF-IDF tokenizers were utilized. These matrixes were fed through NMF and LSA models and after an iterative process, the NMF model using the CountVectorizer doc-term matrix was chosen because it identified the most unique topics (9). 

For classification, I ran the doc-term matrix through a Logistic Regression model for a baseline result then compared it to a Bernoulli Naïve Bayes model and a Multinomial Naïve Bayes model. Unsurprisingly, the Multinomial NB model performed the best:
 
As an extra step, I took the topics as a proxy for the individual tweets and used that as a feature for a traditional classification model, along with other features I engineered. The features were tested on a variety of models with the following results:

![image](https://user-images.githubusercontent.com/77559909/165991807-95927b4c-ca02-4254-9556-4a9679204b77.png)
 
Overall, the XGBoost model actually outperformed all the other traditional classification models and the Naïve Bayes models. I want to caveat the classification models done here because of the small dataset (~5,000 tweets). 

## Tools
Numpy, Pandas, Sciki-learn, Matplotlib, NLTK, RegEx

## Communication
My findings can be found in the presentation and code included in this repo. 
