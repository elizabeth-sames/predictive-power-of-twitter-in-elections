# predictive-power-of-twitter-in-elections
Bootcamp Final Project
We are living in the era of social media. 4.48 billion people currently use social media worldwide and the average time a person spends on social media a day is 2.4 hours. We have nearly uninterrupted instant access to the every thought and opinion of millions of strangers worldwide at any given moment. How can this info be harnessed? What value does it have?

Twitter has 73 million users in the US and about 20% of all tweets are political. Could text analysis of political tweets hold any predictive power in political elections?


THE DATA:
I webscraped presidential and gubernatorial election information from Wikipedia including candidate names, political parties, and the outcomes including the amount of popular votes received.

I used snscrape to webscrape tweets about each candidate for elections from 2006 on. There were very few to no tweets about gubernatorial candidates in the years 2006, 2007, 2008, so I did not use tweet data from those years. I also did not use 2017 due to lack of info about the popular votes.

Voting takes place the first week of November, so I limited my search to tweets from the month of October. As some of the governors had common names, I searched the candidate's name along with keywords such as 'president' or 'governor', and for governors the state.

Presidential elections occur every 4 years, so my dataset included data for 4 presidential elections. Gubernatorial elections occur every 2-4 years depending on the state. My dataset contained data for 156 elections.


EXPLORATORY ANALYSIS:
First I compared the number of tweets about each candidate to the total number of tweets for their election (% total tweets).
Presidential trends: 
- Democrat candidates have a higher % popular vote compared to Republican candidates.
- There does seem to be a positive correlation between % total tweets and % popular vote, at least for 2 main political parties. The other parties showed little to no correlation. 
Gubernatorial trends: 
- There seems to be a stronger positive correlation between the % total tweets and the % popular vote. - - - Again, there are two clusters: the main parties, and the other parties with the other parties showing little to no correlation. 


TWEET SENTIMENT ANALYSIS:
I wanted to explore if the overall sentiment of tweets about a candidate has any predictive power to their election success. I trained a Naive Bayes classifier algorithm on a sentiment labelled tweet sample set from NLTK, (it had a .998 accuracy score) and used it to classify the tweets in my dataset as either positive or negative. 
Presidential findings:
- Slight positive correlation between % positive tweets and % popular vote.
Gubernatorial findings:
- Two clusters: Democratic/Republican parties, and other parties. Tweet sentiment in other parties varies widely but they rarely receive a significant portion of the popular vote.
- Low correlation between % positive tweets and % popular vote.
I was surprised that tweet sentiment seemed to have little correlation with election outcomes. It seemed like the % of total tweets seemed be a stronger predictor of election outcome. 

In order to test the predictive power of these features, I decided to build multiple machine learning regression models to predict the % popular vote of gubernatorial candidates. Then on the most accurate model I looked at the most important features.


THE MODEL:
I used % total tweets, % positive tweets, political party, and state to build the models. I built Linear Regression, Decision Tree, Random Forest, and KNN models. As election outcome is determined by comparing the popular votes of all candidates in that election, I needed to keep candidates grouped by elections when creating the train and test groups. Therefore I did not randomize the groups and I kept all gubernatorial elections from 2018 as the test set as it contained 22% of the total gubernatorial data. 


RESULTS:
The Random Forest was the most accurate predictor of candidate % popular vote wiht a cross-validation score of .92 and lowest rmse score(6.57). 
But, when comparing each elections group of candidate predicted %popular votes, the Decision Tree model was more accurate in predicting the overall winner, correctly predicting the winner through %popular vote in 29 out of 36 elections, compared to 26 for Random Forest and 24 for KNN. The most important features are % total tweets (Score: 0.54113), Republican party (Score: 0.14864), and % positive tweet (Score: (0.03585).


CONCLUSIONS:
The models I built scored well, but I am skeptical about the real-life usefulness of these models. Tweet sentiment did not have the predictive power that I expected. The importance of % total tweets in the models might be a reflection of state partisanship. Most states rarely change their favored political party and the candidate of that party will be the natural frontrunner and likely receive more tweets than other candidates, whether positive or negative. 

The elections that were predicted incorrectly were close elections. So perhaps in order to build a more useful model it would be beneficial to explore those elections and what features led to those outcomes. It could also be beneficial to explore elections where more than two candidates have a realistic chance of winning, such as elections for the House of Representatives or mayoral elections. Or elections in countries with strong multi-party participation.

Another thing to bear in mind when using info from Twitter is the overlap of political tweeters with the demographics of eligible voters. Some vote groups may be over- or under-represented on Twitter. Also there is a vocal minority, 6% of political tweeters account for 70% of political tweets.
