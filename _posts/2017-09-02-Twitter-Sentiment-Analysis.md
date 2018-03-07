---
title: "Twitter Sentiment Analysis"
layout: post
date: 2017-09-02 1:42
image: ../images/Love.png
tag:
- sentimentanalysis
- keras
- rnns
- python
star: false
category: blog
author: kamran
description: Training sentiment analysis model on tweets.
---
# Introduction
With the evolution of deep learning, pretty much every thing has seen drastic change in its functionality. Processes catered by rudimentary computer vision techniques were usually for specialized tasks, were slow and dependent on something or the other. However, due to Deep Learning the results of all those tasks are now much more accurate, the models now generalize, are fast and independent. 

# Recurrent Neural Networks
Recurrent Neural Networks, RNNs, are type of neural networks designed to solve sequence based problems, which they do pretty well. Since every output is dependent on previous input in RNNs, which explains how memory works in RNNs, and they make use of information over long sequences, we use them to solve our problem. We use Long Short Term Memory, LSTM, type of RNNs, which can remember information for a longer period of time. They perform much better than vanilla RNNs. 

With a sequence of words, we predict the probability of next. So, the input is a text and output is a text, this is called a language model.

# Problem
Now that we have the basics clear, we go on to build on the problem we want to solve. 
We want our model to rate the tweets scrapped from twitter in terms of positivity and negativity. We collectively call it polarity. We give polarity an index of [-1,1], where 1 is positive and -1 is negative. 
To explain it a little, the keyword 'love' will be given, let's say, an index of 0.6 and the keyword 'hate' would be given an index of -0.6 and so on. 
We first train the model on the twitter dataset, we then scrap tweets off twitter using keywords and then test the model on them. We finally graph the polarity to visualize how things actually look like. 

# Model
Since we have the problem statement very well defined, we can now go on to think of the model we want to use. LSTMs are well suited for these kind of problems, so, we go on with LSTM. We write the model in Keras, deep learning framework, and then train it. 
Dataset is easily available online, we read the dataset and convert it to embeddings and reshape it so that it can be fed to LSTM. We set the x values to tweets, embedded, and y values to the class labels. There are two labels, positive and negative. This is classification problem since we classify the tweets as positive or negative. We also tokenize the sentences so that they can be converted to embeddings easily. So, finally, our model structure is:

1. Embedding Layer
2. LSTM
3. Dense (Softmax Activation)

The last layer returns the probabilities of the class and that is what we need. We compile the model with categorical crossentopy since we are dealing with a categorical (positive or negative) class problem and then we fit it on the x and y values. 

# Training
We train it for 10 epochs, and then evaluate it over the testing set we separated. After some time of training, we get an accuracy of 78%, which is pretty great. 

# Code
We train the model and save the weights. We then go on to get the api keys from twitter so that we can scrap the tweets. We then do the predictions on those tweets and graph the result. The link to whole code is: <a href="https://github.com/kjanjua26/Twitter_Sentiment_Analysis">Twitter Sentiment Analysis.</a>
The dataset is also given the repo.

# Output
We finally predict the results and graph the output. The following graph is of the keyword 'Love', the output shows that the model works fine. 
{% capture fig_img %}
![Graph](../assets/images/Love.png)
{% endcapture %}

<figure>
  {{ fig_img | markdownify | remove: "<p>" | remove: "</p>" }}
  <figcaption>Graph of keyword 'Love'.</figcaption>
</figure>
