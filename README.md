# csc413-fp-movie-sentiment-analysis

Introduction
This project is a sentiment analysis that classifies the movie reviews as positive or negative with the level of emotion. The model we built is an ensemble with RNN(LSTM+CNN), and Naive-bayes model. We used the original text comments as input in the form of a sequence of words. The output of the model is an integer from 1 to 4 represents negative and from 7 to 10 represents positive.
Model
Figure: 

Parameters: 

Two Examples/prediction from Test set: 
Successful
Unsuccessful
Data
Source: IMDB dataset http://ai.stanford.edu/~amaas/data/sentiment/

Statistics Summary: First we analyzed the level of emotion part of the dataset. The below picture is the analyzed result. Since both mean and median are close to 5, which means neutral emotion, we know that these data are not biased in terms of sentiment, so we can use them. Additionally, we noticed that there are more comments indicating extreme sentiment (such as 1 and 10). With more extreme sentiment comments in the training data, the model will be exposed to a wider range of sentiment expressions, which may help it better distinguish between positive and negative sentiment in test data, then the model accuracy will be improved.

For the word analyze, we discussed it into two parts: keep stopwords and remove stopwords. Stopwords mean these words are commonly used in a language but not meaningful. With stopwords, the most common 10 words are ‘this’, ‘that’, ‘movie’, ‘file’, ‘with’, ‘have’, 'like’, ‘from’, ‘about’, ‘they’. We can see these most common 10 words do not have much emotional bias, so we decided to remove stopwords. Then, the most common 10 words became 'movi', 'film', 'like', 'thi', 'watch', 'time', 'good', 'stori', 'make', 'charact', and the size of vocab is 33917.



Transformation & Split:
- Part 1 


- Part 2 
Each time we read a line from the txt file, we first remove the break symbols “<br/>” and all punctuations. To compress the vocabulary size, we apply additional criterions in processing data, such as removing stop words, digits, incorrect spelling words, and reducing words into the root form. After that, we select the most frequent 1000 words as our vocabulary. Then, we set the maximum length of each sentence to be 100 words. For sentences that are shorter than 100 words, we pad the remaining space with empty string “” so that we have the same input dimension. For sentences that exceed 100 words, we keep the first 100 words in this review because we find out that is enough words to express positive or negative emotion. Since we put target labels at the beginning of each review in the previous step, the read-in dataset has a shape of N*2 where each row has an integer label followed by a list of words.
We split the input vector x and target vector t in the get_batch() function, which takes a dataset and batch size as input. We slice the input dataset by batch size, then convert each word into an index in vocabulary, and lastly make one-hot vectors by indices.


Since the source training dataset is large enough, we decided to keep the provided training set and split the provided test dataset into validation set and test set. In other words, the portion we used to split the training, validation, and test sets is 50%-25%-25%.
Training
Training curve:

Hyperparameter Turning:

Results
Quantitative Measures:

Quantitative and Qualitative Results:

Justification of Results:

Ethical Consideration
One ethical benefit is that it can help audiences know the rating of a movie without being spoiled. Audiences may leave pieces of plot in review on social media, so other audiences can use our model to evaluate the movie based on these reviews without knowing the plot of the movie by accident. However, the dataset may not be balanced in terms of demographics, leading to a biased problem. As different movie themes may appeal to distinct groups of people, they may elicit various emotional responses in reviews that could influence the movie's ratings.

Movie producers can use our model to understand the public's evaluation of their movies based on scattered reviews on social media that may not include a formal rating. This can guide producers to make future decisions regarding marketing and production. However, the ethical issue is movie producers may increasingly rely on sentiment analysis for evaluating audience sentiment, but it should be used in conjunction with other factors and not as the sole determinant.

Also, there are limitations of our model. One limitation is lack of context awareness. Some sentences may have irony or sarcasm. It is hard to determine the real meanings of those sentences without considering the background of those sentences, hence it is hard to classify the movie reviews as positive or negative. Another limitation is lack of topic knowledge. Since our dataset doesn’t include the topic of movies, our model may not accurately generate appropriate ratings for specific movie topics. For example, ‘It makes me cry’ in a horror movie may mean something positive. 

The limitation of our dataset is lack of other forms of comments. For example, many comments will have emojis, pictures, but our dataset only concludes text. Those emojis and pictures also express a lot of meanings, and even some text content with emojis may indicate jokes, irony, etc. Therefore, the lack of these forms of comments will make our rating not entirely accurate.
Authors
Jialin CAI: write the LSTM + CNN model and train models, Tuning hyperparameters, analyze output of models, (in README:) write introduction part, model figure part, model parameters part, model examples part, write data source part, write data split part, write training curve part, write hyperparameter tuning part, write quantitative measures part, write quantitative and qualitative results part, write justification of results part.
Ziyang Qu: write data analysis code, (in README:) write data summary part, write ethical consideration part, write authors part, establish github, submit project.
Yifan QIN: find dataset source, write get accuracy code.
Zeyang WANG: write Naive-bayes model, write data transform code.
