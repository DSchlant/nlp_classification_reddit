## Subreddit NLP Classification

### Background
Many feel that mankind is at an inflection point. Technological progress is rapid: cars are driving autonomously and don't require petrol, mundane tasks are being automated, and AI is utilized across many fields of study. There is much to be excited about. But - how can you be? Updates on the state of the climate become ever more dire, the geopolitical landscape becomes more fraught every day, and the social fabric that binds frays and frays. Where do you feel that civilization is headed? Where might your customers, or the consumers in your next target market?

In an effort to utilize natural language processing (NLP) to try to determine an individual's worldview via their Reddit activity, I used the Reddit Pushshift API to collect posts to two Subreddit pages: r/collapse and r/futurology. The members of each community have self-identified as having conflicting views of the future of humanity. The Futurology Subreddit takes a more positive view on the path forward for humans, technology, and civilization. Members of the collapse community adopt a more pessimistic view for the decades ahead. Below are the respective descriptions for these communities, as stated by their administrators.

#### Collapse of Civilization: r/collapse
Discussion regarding the potential collapse of global civilization, defined as a significant decrease in human population and/or political/economic/social complexity over a considerable area, for an extended time. We seek to deepen our understanding of collapse while providing mutual support, not to document every detail of our demise.

#### Future(s) Studies: r/Futurology
Welcome to r/Futurology, a subreddit devoted to the field of Future(s) Studies and speculation about the development of humanity, technology, and civilization.

### Data Problem
The primary purpose of this analysis will be to develop a model that can accurately identify posts as originating from the Futurology Subreddit or from Collapse, via the text content of the post titles. A secondary, further application would be to apply this analysis to other social media posts or content to assess the author's general outlook on the future of civilization.

### Data Collection
Using Puhsshift API, all posts containing self-text (even if self-text was later removed) were collected from 24 April 2022 back to the inception of the respective subreddits. This provided a wealth of data on both Subreddits: 28,763 posts on Futurology and 28,682 for Collapse. We proceeded with analyzing post titles alone for this study because 32% of the total submissions had self-text removed. It should be noted that the titles of posts for which self-text was removed were still used for analysis. Options for further research include utilizing the available self-text.

### Process
Due to the wealth of available data, a holdout dataset comprising 20% of the available data was set aside to be tested after modeling process completed on training and validation sets.

Initial analysis was run on 30% of the remaining dataset, or 24% of the overall dataset. The dataset was split naturally 50%/50% between Futurology and Collapse, so this served as the initial null baseline. The model will need to demonstrate the ability to choose the correct Subreddit of origin at a higher rate than merely choosing 'Futurology' each time in order to be considered successful.

In creating a custom stoplist for the model, an effort was made to add forms of future/collapse, as well as the subreddit's name. This negatively affected performance. However, it may provide what may be a sounder methodology for identifying an individual's worldview or expectations for the future via their post language.

### Modeling
Many supervised learning models were tested in order to identify the model best fit for classifying the submissions, after either count vectorizing the data or vectorizing the data via TF-IDF. The models studied included:

* Multinomial Naive Bayes
* Gaussian Naive Bayes
* Logistic Regression
* K Nearest Neighbors Regression
* Decision Tree 
* Random Forest
* AdaBoost
* Ensemble Analysis

The best performing model incorporated **Naive Bayes and TF-IDF vectorization**. 

### Results
The model had an **accuracy rate of 81.68% on the validation set**. The model performed with **81.28% accuracy on the holdout set**, which is 20% of the overall dataset initially scraped from Reddit. This is well above the 50.3% baseline derived from the percentage of the majority class in this dataset.

### Qualitative Analysis
The language used on the r/collapse subreddit was community oriented, supportive, humorous, profane, and concerned with climate change. The subreddit also had a strong survivalist tone. The language used on the r/futurology subreddit was very much concerned with longevity and extending life, automation and robotics, and how best to use the additional leisure time that a more automated world would provide.

### Conclusion
The model developed can predict whether Reddit user's post was intended for a techno-positive, optimistic forum or a thread with a more fatalistic view with 82% accuracy when introduced to new posts. As the model encounters more data, accuracy improves. Using the findings of this NLP model may provide insight into a user's worldview or expectations of the future based on text that they have produced.

### For Further Research
#### Self-Text Analysis
Quick analysis was performed using the same Naive Bayes model on both the title and self-text data. Titles alone were used for the previous analysis since self-text had been removed for such a large percentage of the posts. When the available self-text was added to the model and some hyperparameters tuned, the model achieved 84.71% accuracy on the validation set and 84.64% accuracy on the holdout set.

#### Sentiment Analysis
Develop and add sentiment analysis to model so model can better assess author's tone or intent. May lead to more accurate modeling, especially when the classes to be identified contain similar text, as was the case in this study.

#### Expand Research to other Subreddits
This study partially intended to develop an understanding of the language used by Reddit users who identify themselves as having a certain worldview. Incorporating additional subreddits in which users have similar attitudes could contribute to the development of a model that can predict a user's worldview based on their activity on other platforms or forums.  

### Further Reading
* https://towardsdatascience.com/text-vectorization-term-frequency-inverse-document-frequency-tfidf-5a3f9604da6d
* https://www.linkedin.com/pulse/count-vectorizers-vs-tfidf-natural-language-processing-sheel-saket/
* https://jakevdp.github.io/PythonDataScienceHandbook/05.05-naive-bayes.html

