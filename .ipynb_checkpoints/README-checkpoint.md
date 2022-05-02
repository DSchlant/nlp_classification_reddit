**Subreddit NPL Classification Modeling**

Many feel that humanity is at a major inflection point. Technological progress is rapid: cars are driving themselves and running on electricity, mundane tasks are being automated, and AI is contributing to providing solutions across many fields of study. There is much to be excited about. But - how can you be? Every week, updates on the state of the climate become more dire, the geopolitical landscape becomes more fraught, and the social fabric that binds us all together seems to fray. Where do you feel that civilization is headed? Where might your customers? Or the members of your next target market?

In an effort to utilize natural language processing (NPL) to try to determine an individual's worldview via their Reddit activity, we have used the Reddit Pushshift API to collect submissions to two Subreddit pages: r/collapse and r/futurology. The members of each community have self-identified as having conflicting views of the future of humanity. The Futurology Subreddit takes a more positive view on the path forward for humans, technology, and civilization. Members of the collapse community adopt a more pessimistic view for the decades ahead. Below are the respective descriptions for these communities, as stated by their administrators:

**Collapse of Civilization**
*r/collapse*
Discussion regarding the potential collapse of global civilization, defined as a significant decrease in human population and/or political/economic/social complexity over a considerable area, for an extended time. We seek to deepen our understanding of collapse while providing mutual support, not to document every detail of our demise.

**Future(s) Studies**
*r/Futurology*
Welcome to r/Futurology, a subreddit devoted to the field of Future(s) Studies and speculation about the development of humanity, technology, and civilization.


***Problem Statement***
The primary purpose of this analysis will be to develop a model that can accurately identify posts as originating from the Futurology Subreddit ot from Collapse, via the text content of their titles. A secondary, further application would be to apply this analysis to other social media posts or content to assess the author's general outlook on the future of civilization.

***Data Collection***
Using Puhsshift API, collected Subreddit submissions that contained self-text from Sunday April 24th back to the inception of the subreddits provided a wealth of data on both Subreddits: 28,876 posts on Futurology and 28,741 for Collapse. We proceeded with analyzing post titles alone for this study because 32% of the total submissions had self-text removed. Options for further research include utilizing the available self-text, as well as the titles for historic submissions that do not include self-text.

***Process***
Due to the wealth of available data, a holdout dataset comprising 20% of the available data was set aside to be tested after modeling process completed on training and validation sets.

Initial analysis was run on 30% of the remaining dataset, or 24% of the overall dataset. The dataset was split virtually 50%/50% between Futurology and Collapse, so this served as the initial null baseline. The model will need to demonstrate the ability to choose the correct Subreddit of origin at a higher rate than merely choosing 'Futurology' each time in order to be considered successful.

In creating a custom stoplist for the model, an effort was made to add forms of future/collapse, as well as the subreddit's name. This negatively affected performance. However, it may provide what may be a sounder methodology for identifying an individual's worldview or expectations for the future via their post language.

***Modeling***
Many supervised learning models were tested in order to identify the model best fit for classifying the submissions, after either count vectorizing the data or vectorizing the data via TF-IDF. The models run included:

* Multinomial Naive Bayes
* Gaussian Naive Bayes
* Logistic Regression
* K Nearest Neighbors Regression
* Decision Tree 
* Random Forest
* AdaBoost
* Ensemble Analysis

The best performing models incorporated Naive Bayes, with the model utilizing TF-IDF vectorization being the most accurate. Further reading regarding TF-IDF vectorization provided by experienced data scientists can be found below. TFI-DF does not necessarily rely on word count alone. The method provides more weighting to a word if it occurs often in a certain submission title, but will reduce its influence in the model if that same word shows up in many of the titles.

Naive Bayes Classifier is a supervised learning method that will generate the probability that, in this context, a post belongs to a certain thread given the words that are in the title, and selects the thread with the highest probability. This is a simple explanation, but further reading can be found below as well.

***Results***
This model, after incorporating the customized list of stop-words, generated an accuracy rate of the test set (using 30% after the holdout was removed) of 80.8%. Using just the list of standard English stop-words yielded an accuracy rate of 82.3% on this test set.

When this model was fit run on 100% of the training/validation dataset, the model had an accuracy rate of 82.8%, improving as the model saw more data. The model performed with **81.67% accuracy on the holdout set**, which is 20% of the overall dataset initially scraped from Reddit. This is well above the 50.3% baseline derived from the percentage of the majority class in this dataset.

***Qualitative Analysis***
Qualitative analysis of the words and terms with the most impact on the model were telling:
* Collapse Subreddit
    * Community-oriented, supportive
    * Strong survivalist community
    * Humorous, profane
    * Climate Change obsessed

* Futurology Subreddit 
    * Extending life, longevity
    * Automation/robotics 
    * Luxury, leisure oriented


***Conclusion***
We have developed a model that can predict whether Reddit user's post was intended for a techno-positive, future-optimistic forum or a thread with a more fatalistic view with 82% accuracy when introduced to new data. As the model encounters more data it improves in its accuracy. Using the findings of this NLP model may provide companies insight into a user's worldview or expectations of the future based on text that they have produced.

***For Further Research***
*Self-Text Analysis*
Quick analysis was performed using the same Naive Bayes model on both the title and self-text data. Titles alone were used for the previous analysis since self-text had been removed for such a large percentage of the posts. When the available self-text was added to the model and some hyperparameters tuned, the model achieved 84.64% accuracy on the validation set.

*Sentiment Analysis*
Develop and add sentiment analysis to model so model can better asses author's tone or intent. May lead to more accurate modeling, especially when the classes to be identified contain similar text, as was the case in this study.

*Expand Research to other Subreddits*
This study partially intended to develop an understanding of the language used by Reddit users who identify themselves as having a certain worldview. Incorporating additional subreddits with similar attitudes could contribute to the development of a model that can predict a user's worldview based on their activity on other platforms or forums.  

***Further Reading***
* https://towardsdatascience.com/text-vectorization-term-frequency-inverse-document-frequency-tfidf-5a3f9604da6d
* https://www.linkedin.com/pulse/count-vectorizers-vs-tfidf-natural-language-processing-sheel-saket/
* https://jakevdp.github.io/PythonDataScienceHandbook/05.05-naive-bayes.html

