# 🤖AI-Powered Movie Recommendation System

Project Objective
------------
The goal of this project is as follows -

1) **Binary and Multi-class Sentiment Analysis.**

2) **Movie Recommendation System.**

This readme first goes through the sentiment analysis part, followed by discussion on recommendation system in the second part. Overall outline of the project is given as follows -

<img src="outline.png" width="800">

Binary and Multi-class Sentiment Analysis System
------------
### Used Datasets

We have used two datasets for sentiment analysis task. 

<ul>
<li>IMDB Reviews dataset with binary sentiment labels (Positive, Negative reviews)</li>
<li>Tweets dataset with 3-way sentiment labels (Pleasant, Unpleasant, Neutral)</li>
</ul>

For the sentiment analysis part, we have used **two** approaches.
<ul>
<li> Machine learning approach
<li> Deployed NLP Models
</ul>

### Machine learning approach

There are two models used for sentiment analysis and classification under normal machine learning approach
<ul>
<li> Random Forest
<li> Logistic regression
</ul>

#### Random Forest
Random Forest is the collection of many decision trees where at each candidate split in the learning process, a random subset of the features is taken. We have used this technique to see the overall important words for classification of sentiments.

#### Logistic Regression
Logistic Regression is one of the effective model for linear classification problems. Logistic regression provides the weights of each features that are responsible for discriminating each class.

Below are the word cloud visualization for IMDB datasets using Random Forest and Logistic Regression.

<img src="wordcloudafterclassifier.png" width="200">

**Important words for sentiment classification.**

<img src="wordcloudLogRegressionPos.png" width="200">

**Important words for positive class.**

<img src="wordcloudLogRegressionNeg.png" width="200">

**Important words for negative class.**

Below are the word cloud visualization for twitter using Logistic Regression.

<img src="neturalBalanced.png" width="200">

**Important words for neutral class.**

<img src="pleasantBalanced.png" width="200">

**Important words for pleasant class.**

<img src="unpleasantBalanced.png" width="200">

**Important words for unpleasant class.**

### Deployed NLP Models

For sentiment analysis modeling, we have employed **three deep NLP** based models, as follows -

<ol>
<li>Recurrent Neural Network (RNN) Based (aka The Baseline)</li>
<li>Your Average Sentiment Network (aka AvgNet)</li>
<li>Convolutional Neural Network (CNN) Based (aka CNet)</li>
</ol>

Next, we briefly explain these three models and their training and evaluation details.

#### 1. Recurrent Neural Network (RNN) Based (aka The Baseline)

This is the first NLP based model for sentiment analysis task. It consists of Recurrent Neural Network (RNN) based nodes with learnable parameters. First, each word is vectorized using a dictionary vector, followed by passing through the 100-D per word embedding layer. Then, we have RNN nodes, outputting hidden state (next layer input). Finally, the last hidden state output passes through the fully connected (FC) layer to yield the sentiment result.

<img src="the_baseline2.png" width="700">

#### 2. Your Average Sentiment Network (aka AvgNet)
    
This model works similar to the above, except it uses **Global Average Pooling** insted of RNN nodes. Consequently, it works faster and detailed in this paper.

<img src="bigrams_model.png" width="700">

#### 3. Convolutional Neural Network (CNN) Based (aka CNet)

This model uses convolutional neural network (CNN) absed approach instead of conventional NLP/RNN method. But still very effective as shown in the evaluation and performance section later. This model has been taken from this paper.

<img src="cnn_model.png" width="700">

### NLP Models Hyper-Parameters

ALl three NLP models (Baseline, AvgNet, CNet) have been trained using pre-defined **hyper-paramters** as listed in following table. It may be noted that these hyper-parameters have been selected after performing several **ablation experiments using orthogonalization process**.

<img src="hyper_params.png" width="600">

NLP Models on IMDB Reviews Binary sentiment dataset
------------

IMDB Reviews dataset is a binary sentiment dataset with two labels (Positive, Negative). Above three NLP models are trained and evaluated on IMDB Reviews dataset separately. Following graphs show their training loss and training accuracy graphs first one by one.

<img src="baseline_train.png" width="700">
<img src="model1_train.png" width="700">
<img src="model2_train.png" width="700">

#### As shown above, the baseline is not doing very good in training and testing phases. AvgNet and CNet shine with good accuracy and other evaluation metrics. 

IMDB Reviews dataset Automated WordCloud Generation using NLP Models
------------

Once we have the models trained and evaluated, here, we analyze and compare the **word cloud** for both sentiments (Positive, Negative) with the ground truth word cloud for both sentiments. Each two rows below shows the comparison of **ground truth word cloud and our three NLP models** respectively.

#### Recurrent Neural Network (RNN) Based (aka The Baseline)

<img src="wcloud_baseline1.png" width="700">

#### Your Average Sentiment Network (aka AvgNet)

<img src="wcloud_model1.png" width="700">

#### Convolutional Neural Network (CNN) Based (aka CNet)

<img src="wcloud_model2.png" width="700">

NLP Models on Tweets Multi-class sentiment dataset
------------

Tweets dataset is a **multi-class (3-way) sentiment tweets dataset** with 3 labels (Pleasant, Unpleasant, Neutral). **Since the AvgNet gave one of the best results, so to avoid redundancy, we only trained and evaluated AvgNet on Tweets dataset.** Following graphs show the AvgNet training loss and training accuracy graphs first on Tweets dataset.

<img src="model1_train_tweets.png" width="700">

#### AvgNet again gives reasonable acurracy, precision and recall values of 92.51%, 0.93 and 0.93 respectively. 
**Word Cloud** for all three sentiment labels are shown below and also being compared with their ground truth in each of the below row.

<img src="wcloud_model1_tweets.png" width="700">

Recommendation System
------------

First, we scraped **OMDb API** to derive more features for the recommendation system.

API link - http://www.omdbapi.com/

**OMDb API** is an open API, which provides a dataset of IMDB movies with numerous features. We have selected **genres** and **ratings** as these features made more sense than the features like **language**. As shown in the following diagram, it doesn't make much sense to select language as there are far more English movies as compared to other languages.

<img src="languages.PNG" width="700">

We used following three models for the movie recommendation system.

<ul>
<li>K-means clustering</li>
<li>Agglomerative clustering</li>
<li>DBSCAN clustering</li>
</ul>

Conclusion
------------

We performed two different tasks during this project, Binary/Multi-class Sentiment Analysis and Movies Recommendation system. During seniment analysis task, we tried both conventional Machine Learning algorithms (Logistic Regression, Random Forest) as well as current state-of-the-art deep learning based NLP methods (RNN Baseline, AvgNet, CNet). We observed that both types of methods perform pretty effective with reasonable results and accuracy. Also, the automated wordcloud plots give valuable insights about the sentiment present in the used datasets. The automated sentiment extraction process from movie reviews or tweets can prove really helpful for businesses in improving their products based on customer's reviews and feedback with much efficiency and effectivness.
