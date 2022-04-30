The subreddits that I have elcted to analyze are the r/collapse and r/futurology pages.

Ostensibly the members of each community have conflicting views of the future of humanity. The futurology subreddit takes a more positive view on the path forward for humans, technology, and science. Members of the collapse community take a more pessimistic view for the decades ahead. Below are their respective descriptions:

Collapse of Civilization
r/collapse
Discussion regarding the potential collapse of global civilization, defined as a significant decrease in human population and/or political/economic/social complexity over a considerable area, for an extended time. We seek to deepen our understanding of collapse while providing mutual support, not to document every detail of our demise.


Future(s) Studies
r/Futurology
Welcome to r/Futurology, a subreddit devoted to the field of Future(s) Studies and speculation about the development of humanity, technology, and civilization.


The primary purpose of this analysis will be to develop a model that can accurately identify posts as originating from one subreddit or the other. A secondary, further application would be to use this analysis and apply it to other social media posts or content in an effort to us the model to assess the author's general view on the future of the Earth and humanity.

Pulling the submission containing self-text from Sunday April 24th back to the inception of the subreddits provided a wealth of data on both subreddits: 28,876 on Futurology and 28,741 for Collapse. Upon reviewing the 'self-text' column, I found a multitude of removed posts - meaning the posts had either been removed permanently, or had been automatically removed by a mod and then subseuqnetly reposted. There were over 11,000 such removed self-text field for Futurology and over 7,000 for Collapse. Thus, I elected to proceed with analyzing the post title alone for this project.

Because I had a wealth of data, I decided to set aside a holdout dataset after I had combined and shuffled the two subreddit datasets. I set aside 20% of the dataset to serve as a holdout.

Due to the size of the available dataset, and concerns regarding computation time, I decided to run my initial analysis on 30% of the remaining dataset, or 24% of the overall dataset. This was 13,828 post titles - fairly evenly split between the two subreddits: 6920 to futurology, 6908 to collapse. This is essentially a 50% split, so this served as the initial null baseline. The model will need to demonstrate the ability to choose the correct subreddit of origin at a higher rate than merely choosing 'Futurology' each time.

In creating a custom stoplist for the model, an effort was made to add forms of future/collapse, or formats that the subreddit name may be included in the posts so that the model would not have an unnatural advantage. This negatively affected performance, of course, but provides what may be a sounder methodoloy.

With the data in hand, I proceeded to run many variations of models in order to find the model that generates the most accurate predictions, after either count vectorizing the data or vectorizing the data via TF-IDF.. The models run included:

* Multinomial Naive Bayes
* Gaussian Baive Bayes
* Logistic Regression
* K Nearest Neighbors Regression
* Decision Tree 
* Random Forest
* AdaBoost
* Ensemble Analysis

This analysis yielded 


