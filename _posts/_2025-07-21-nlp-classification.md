---
layout: post
title: Yelp Reviews Sentiment Analysis
subtitle: Natural Language Processing using NLTK
cover-img: https://sbmi.uth.edu/blog/imgs/14-word-cloud-3-351x195.jpg
thumbnail-img: https://sbmi.uth.edu/blog/imgs/14-word-cloud-3-351x195.jpg
share-img: /assets/img/path.jpg
tags: [classification analysis, pandas, scikit-learn, nltk]
---

### Introduction
The goal of this project is to perform sentiment analysis ( to label a review "positive", "negative", or "neutral" ) using natural language processing (NLP) on Yelp reviews dataset. Natural language processing (NLP) is the method by which computers make sense of written text. Sentiment analysis, a subfield of NLP, involves predicting the tone of a text. There are many reasons to understand the opinion expressed in text. Sentiment analysis can be useful for businesses trying to understand customer feedback, for a company launching a new product, or for determining the underlying emotion behind a stock. The analysis was performed across two jupyter notebooks which can be accessed on the project's [github repository](https://github.com/biman-zen/nlp-sentiment-analysis). 

### Dataset
The [Yelp reviews dataset](http://www.yelp.com/dataset_challenge) was developed for the 2015 Yelp Challenge and consists of reviews of businesses. The dataset is sourced from [hugging face](https://huggingface.co/datasets/Yelp/yelp_review_full). The dataset consists of two .csv files: *training.csv* with 650k records and *test.csv*. with 50k records. Although the feature engineering of the dataset was not needed, the necessary text preprocessing to normalize the data takes nearly an hour. 

### DW & EDA
There's little data wrangling required for text-based datasets for NLP in comparison to numerical and categorical datasets. For datasets with text features like this there is no need to perform in depth data wrangling or exploratory data analysis as with traditional datasets with many numerical and categorical features (e.g. car dataset).
The dataset has two features the number of stars (1-5) and the text review. The histogram below shows that the dataset includes an equal number of stars. 
![star-dist]({{"/assets/post_figures/sentiment-analysis/distribution_of_stars.png" | relative_url }}){:style="width: 60%; height: auto; display: block; margin: 0 auto;"}

The distribution of review count length shows each star has a mean around 700 characters and skews right.
![kde]({{"/assets/post_figures/sentiment-analysis/dist_kde_plot.png" | relative_url }}){:style="width: 60%; height: auto; display: block; margin: 0 auto;"}

#### Text Normalization
Normalization is the process that brings text into a standard format to extract meaning from. The text is broken down to tokens which can be words but can also be multiple words depending on the strategy. These token words can be further standardized using a method called lemmatization i.e. reducing the word to its root base form, as found in a dictionary. Standardization involves lower casing, removing stop-words, and performing lemmatization. NLTK is a natural language processing library that is used to perform all the necessary processing to the review text. The following is a python function used to standardize the review text. For each review, the text is lower-cased, then the punctuations and stop words are removed, and then each word is lemmatized. 

    def preprocess_text(text):
        # Tokenize the text
        tokens = word_tokenize(text.lower())

        # Remove stop words and punctuations in the tokens list
        stp_wrds_puncts = list()
        stp_wrds_puncts.append(string.punctuation)
        stp_wrds_puncts.extend(stopwords.words('english'))
        filtered_tokens = [token for token in tokens if token not in stp_wrds_puncts]

        # Lemmatize the tokens
        lemmatizer = WordNetLemmatizer()
        lemmatized_tokens = [lemmatizer.lemmatize(token) for token in filtered_tokens]

        # Join the tokens back into a string
        processed_text = ' '.join(lemmatized_tokens)

        return processed_text  

#### BOW and TF-IDF 
Normalized tokens counted in terms of frequency is referred to as the bag of words approach. BOW is a simple frequency count of meaningful words. TF-IDF is a more robust method than BOW for vectorizing text as it attempts to look at how rare a word is as well as how frequent the word appears. The TF-IDF score for each word in a document is determined by multiplying its Term Frequency (TF) and its Inverse Document Frequency (IDF). The following is a TF-IDF score of the top 20 words for 1k sample one-star and five-star reviews. Note that there is an overlap of the words int eh one-star and five-star reviews. The overlap occurs because the alogrithm does not understand the difference between good and not good or not bad and pretty bad. An assumption was made that (1,2) stars are a negative sentiment, a 3 stars equated to a neutral sentiment, and (4,5) stars are a positive sentiment. The processed reviews were then vectorized to create features using TF-IDF.
![tfidf]({{"/assets/post_figures/sentiment-analysis/tfidf_bar_plot.png" | relative_url }}){:style="width: 60%; height: auto; display: block; margin: 0 auto;"}

### Model
VADER, a model from the NLTK library, is a rule-based sentiment analysis tool can output a numerical value based on 'positive' or 'negative'. VADER stands for Valence Aware Dictionary and sEntiment Reasoner. NLTK's *'SentimentIntensityAnalyzer'* function which uses VADER was used to perform sentiment analysis on the processed reviews. The following function is a snippet that extracts the analyzed sentiment from the normalized text. 

    def get_sentiment(text_list):
        # Determine the sentiment of entire training set
        analyzer = SentimentIntensityAnalyzer()    
        sent_results = list()
        # Loop through dataframe processed text to get sentiment
        for text in tqdm(text_list):
            # Get the sentiment polarity from text
            scores = analyzer.polarity_scores(text)
            # Condition for sentiment results
            if scores['compound'] > 0.75:
                sentiment = 'positive'
            elif scores['compound'] < -0.75:
                sentiment = 'negative'`
            else:
                sentiment = 'neutral'
            # Create list of sentiment
            sent_results.append(sentiment)

The following is the calculated sentiment for the train and test datasets. Note that while the one star reviews have the highest percentage of negative sentiment, the positive sentiment dominates across all star levels. The *'SentimentIntensityAnalyzer'*, which outputs values from -1 to +1, was adjusted to a narrower threshold. Regardless of adjustment, the positive classifier still dominated.  
![sentiment]({{"/assets/post_figures/sentiment-analysis/sentiment_results.png" | relative_url }}){:style="width: 75%; height: auto; display: block; margin: 0 auto;"}

### Results
Thus far, the text in the dataset have been normalized and then converted to a sentiment value. Multi-nomial classifier ML models are needed to map the true sentiment (stars) to the calculated sentiment. Three ML models: Logistic regression, SVM, Naïve Bayes, and Random Forest were used to perform multinomial classification. Multinomial classifiers are able to predict more than two categories. A comparison of the results was performed shows that SVC classification model performed the best outcome with an accuracy of nearly 73%. Note that although the "logistic regression" model has "regression" in the name, it is confusingly a classifier model.
![5foldCV]({{"/assets/post_figures/sentiment-analysis/five_foldCV_results.png" | relative_url }}){:style="width: 60%; height: auto; display: block; margin: 0 auto;"}

The following confusion matrix of SVC model, which had the best results out of the three models, shows the model's prediction capability. Although the model is capable of predicting positive and negative review at a f1-score of 80%, it struggles to classify a neutral reviews (45%).  
![confmatrix]({{"/assets/post_figures/sentiment-analysis/linear_svc_results_confusion_matrix.png" | relative_url }}){:style="width: 60%; height: auto; display: block; margin: 0 auto;"}

This NLP project tried to extract sentiment from Yelp reviews and correlate this to the number of stars of the review. While the multinomial models fit the mapped data well, the sentiment analyzer was unable to correlate the sentiment to the star rating.
Find the project files on the [github repository](https://github.com/biman-zen/nlp-sentiment-analysis).
