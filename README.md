# SentimentAnalysis
## 🛈 Background Information
Sentiment analysis is a branch of natural language processing that involves determining the sentiment - or emotional tone - expressed in a piece of text. It aims to classify the sentiment as positive, negative, or neutral. Originating in the early 2000s, sentiment analysis has evolved with advancements in machine learning and linguistic techniques, enabling applications in various domains such as social media monitoring, customer feedback analysis, and brand reputation management.

The NBA Finals is a prestigous event which crowns the best professional basketball team in the world on a yearly basis. With this prestige comes pressure filled moments, emotional turmoil, and lots of interviews to capture it all! Let's take one of the biggest stars in basketball, Lebron James, and perform sentiment analysis on his interviews during each of his trips to the NBA Finals. 

Lebron James has made 10 seperate Finals appearances. This is a man who competed in 8 consecutive NBA Finals; we are talking about greatness here! Not only is he one of the greatest players of all time, he is viewed as one of the greatest role models as well. An activist, entrepreneur, father, and above all, a human being, LeBron James has been in the spotlight since his mid-teenage years, serving as a shining example for all who observe him.

## 🎯 Aim


## :robot: ChatGPT
Prompt testing was initially performed on openai's website. We found most consistent results when submitting batches of 5 questions/responses. After a consistent return from our prompt, we integrated ChatGPT into Python and identified the tone of over 2,000 questions and responses. Prompt: "Let 1 = positive, 0 = neutral, and -1 = negative. Identify the tone of the 5 questions using the given values. Output the list of values in order of the questions."

Originally an f-string was used to auto generate the number of questions (as we send batches of 5, but inevitably are left with a 'remainder' group ranging in size of 1-5). This, however, increased token usage and so a while loop was utilized to send the prompt which matched the number of questions. Overall, ChatGPT performed well only returning an error on 3 of the over 100 interviews submitted. 

## :mag_right: Interview Source
http://www.asapsports.com/show_player.php?id=13888

## :triangular_ruler: Skills and Methods
**Web Scraping** - Performed web scraping through the use of the bs4 library. Encoding detectors were used to identify all links on the page and BeautifulSoup package was utilized to pull all text from the selected links. Used understanding of website tags to scrape desired text; we scraped 'i', 'h3' and 'td' tags as the format varied - a variation due to the fact that some of these interviews are over 15 years old. Scraped headers from each page to identify the date and interview type (game or practice).       

**Text Cleaning** - Once we aggregate the text from each interview we are ready to begin processing our data.  

**DataFrame Creation** -

**Regression Analysis** - 

## :children_crossing: Walkthrough 

## :closed_book: Conclusion
We began by transforming interview transcripts of Lebron James during the NBA Finals into meaningful quantitative data. We identified the tone of each question and response from all such interviews utilizing ChatGPT. We then created variables 'response rating' and 'question rating' which summed the response/question tones (values of -1, 0, 1 assigned by ChatGPT) for each interview and divided by the total number of responses/questions. Each of these features are linear and thus we perform linear regression on them; resulted in an R^2 value of .271, which is less than ideal.

Next, we form more features as we work to improve our correlation coefficient and eventually our accuracy on test data. We identify that 'question rating' is a complex feature which is partially described by other features, and decide to avoid using it. Our features with the strongest relationship to Lebron James' response rating were 'cumulative wins', 'cumulative losses', 'win', and 'loss'. This combination obtained an adjusted R^2 score of .419, a substantial improvement over the linear variation and an acceptable value when studying information which falls under social sciences. A Durbin-Watson score of 2.125 implies we are safe from autocorrelation, and an F-statistic of 19.38 is large enough to imply that our model is significant. 

Utilizing multivariate regressional analysis on test data we obtained an average residual of only 0.06. When converting this data into binary classification we obtained an accuracy score of 80.95%. Lastly, we performed the same analysis on the data excluding practice interviews and reached an accuracy score of 90.90%. Further validating our intuition that the data would be "too predictable" without the practice interviews.

## :construction: Improvements
