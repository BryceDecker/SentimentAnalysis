# SentimentAnalysis
## 🛈 Background Information
Sentiment analysis is a branch of natural language processing that involves determining the sentiment - or emotional tone - expressed in a piece of text. It aims to classify the sentiment as positive, negative, or neutral. Originating in the early 2000s, sentiment analysis has evolved with advancements in machine learning and linguistic techniques, enabling applications in various domains such as social media monitoring, customer feedback analysis, and brand reputation management.

The NBA Finals is a prestigous event which crowns the best professional basketball team in the world on a yearly basis. With this prestige comes pressure filled moments, emotional turmoil, and lots of interviews to capture it all! Let's take one of basketball's biggest stars, Lebron James, and perform sentiment analysis on his interviews during each of his trips to the NBA Finals. 

Lebron James has made 10 seperate Finals appearances. This is a man who competed in 8 consecutive NBA Finals; we are talking about greatness here! Not only is he one of the greatest players of all time, he is viewed as one of the greatest role models as well. An activist, entrepreneur, father, and above all, a human being, LeBron James has been in the spotlight since his mid-teenage years, serving as a shining example for all who observe him.

## 🎯 Aim
As mentioned, we aim to perform sentiment analysis on Lebron's interviews conducted during his appearances in the NBA finals. 

Our initial objective is to convert interview text from a website into clean and organized text, which will be stored in a list format using Python. This data preparation step is necessary to ensure that our data is ready to be inputted into ChatGPT, where the subsequent sentiment analysis will be carried out.

Following the analysis, we must identify the most appropriate feature which influences Lebron's response tone. We will utilize this feature to perform linear regression.

When examining tone, it is essential to acknowledge the presence of numerous influential factors. Through feature analysis we aim to find the most impactful features and use these to perform multivariate regression analysis.

After conducting the regression analysis, we will assess the outcomes and subsequently further our understanding by transforming these results into binary classification.

Lastly, we will perform all of the aforementioned mentioned techniques again, but first removing interviews from practice days. This will help in comprehending the variation in our models' predictions caused by these interviews.

## :robot: ChatGPT
Prompt testing was initially performed on openai's website. We found most consistent results when submitting batches of 5 questions/responses. After a consistent return from our prompt, we integrated ChatGPT into Python and identified the tone of over 2,000 questions and responses. 

Prompt: "Let 1 = positive, 0 = neutral, and -1 = negative. Identify the tone of the 5 questions using the given values. Output the list of values in order of the questions."

Originally an f-string was used to auto generate the number of questions (as we send batches of 5, but inevitably are left with a 'remainder' group ranging in size of 1-5). However, this led to an increase in token usage. To address this, we implemented a while loop to send the prompt that matched the number of questions. Overall, ChatGPT performed well only returning an error on 3 of the over 100 interviews submitted. 

## :mag_right: Interview Source
http://www.asapsports.com/show_player.php?id=13888

## :triangular_ruler: Skills and Methods
**Web Scraping** - We conducted web scraping using the bs4 library, utilizing encoding detectors to identify all the links on the page. The BeautifulSoup package was employed to extract the text from the selected links. Leveraging my understanding of website tags, I targeted specific text elements, scraping 'i', 'h3', and 'td' tags to account for the varied formatting, given that some of these interviews date back over 15 years. Additionally, I extracted the headers from each page to identify the date and interview type (game or practice).  

**Text Cleaning** - Once we aggregate the text from each interview we are ready to begin processing our data.  

**DataFrame Creation** -

**Regression Analysis** - 

## :children_crossing: Walkthrough 

## :closed_book: Conclusion
We initiated the sentiment analysis process on Lebron James' NBA Finals interviews by leveraging the capabilities of ChatGPT. We then created variables 'response rating' and 'question rating' which summed the response/question tones (values of -1, 0, 1 assigned by ChatGPT) for each interview and divided by the total number of responses/questions. Since each of these features exhibits linearity, we conducted linear regression analysis, which yielded an $R^2$ value of .271. However, this value falls below the desired range, indicating a suboptimal fit.

Subsequently, we proceed to identify and incorporate additional features with the aim of enhancing our correlation coefficient and ultimately improving the accuracy on our test data. After recognizing that 'question rating' is a complex feature and is partly explained by other features, we make the decision to exclude it from our analysis. Our features with the strongest relationship to Lebron James' response rating were 'cumulative wins', 'cumulative losses', 'win', and 'loss'. This combination obtained an adjusted $R^2$ score of .419, a substantial improvement over the linear variation and  proves to be a satisfactory value when examining information within the realm of social sciences. A Durbin-Watson score of 2.125 implies we are safe from autocorrelation, and an F-statistic of 19.38 is large enough to imply that our model is of significance. 

Utilizing multivariate regressional analysis on test data we obtained an average residual of 0.06. When converting this data into binary classification we obtained an accuracy score of 80.95%. Lastly, we performed the same analysis on the data excluding practice interviews and reached an accuracy score of 90.90% (correctly predicting 10 of the 11 data points). Further validating our intuition that the data would be "too predictable" without the practice interviews.

## :construction: Improvements
