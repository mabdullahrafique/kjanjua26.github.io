---
layout: post
title: Generating Shakespeare Poetry
tags: [keras, poetry generation, blog]
---

# Introduction
Generating texts is rather an important problem in machine learning domain. It is important to build models so that they are able to learn from the text and then generate the same style prose or poetry.

# Problem
Considering the advances made in deep learning, we train a model on Shakespeare's works and then try to re-produce it.
As we know that this is again a sequence-to-sequence problem, a language model, we can, therefore, use RNNs to solve this problem. 
We have different options i.e. GRU, LSTMs, SimpleRNNs in RNNs to chose from, we go with Long Short Term Memory aka LSTM. 
LSTM performs like, if not better, GRU and thus it is our option. 
We use Keras, deep learning framework, to write and train the model. 

# Dataset
For every problem we solve using Deep Learning, we need tons of data to begin with. Thanks to Andrej Karpathy, we can get Shakespeare's work in a simple text file and thus can train our model on it. The data set is called *Tiny Shakespeare*, since it is a portion of Shakespeare's works. 
Check out his repository: <a href="https://github.com/karpathy/char-rnn">Karpathy's Repo</a>

Once we download the dataset, we see that it is simple .txt file with Shakespeare's work written. An example is: 
 
*First Citizen:*
*Before we proceed any further, hear me speak.*
*All:*
*Speak, speak.*
*First Citizen:*
*You are all resolved rather to die than to famish?*
*All:*
*Resolved. resolved.*

# Dataset Formatting
We now focus on formatting the text file so that we can feed it into LSTM. We know that we cannot directly feed the text to model since it won't understand, instead, we will convert the whole text to corresponding numbers, embedded the text and form vectors. This is called *word2vec* or Word to Vector representation. 
We first convert the chars to integers. 
`ci = dict((c,i) for i,c in enumerate(chars)) #chars to int`

We now append those to x and y arrays. There is no validation since we just calculate the loss and then generate the text after loading the saved model. 

	`for i in range(0, num_c - seq_len, 1):
	s_in = data[i:i + seq_len]
	s_out = data[i + seq_len]
	x.append([ci[char] for char in s_in])
	y.append(ci[s_out])`

# Training
Once we have formatted the dataset, we now go on to build the model for training. We stack LSTM layers, add dropout and fully connected at the end followed by softmax. We use *adam* optimizer and train on 40 epochs. We fit the model on x and y and then train it. 

# Output
After about a week of training, we get the loss down to approx. 1.5, this is great to begin with. 
We then generate the text using the saved model.  

# Code
The github repository link is: <a href="https://github.com/kjanjua26/Shakespeare-Poetry-Generation">Shakespeare Poetry Generation</a>
