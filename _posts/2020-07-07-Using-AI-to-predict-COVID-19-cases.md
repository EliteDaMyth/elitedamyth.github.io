---
layout: post
title: Predicting Number of COVID-19 Cases using AI!
subtitle: So I made a Deep Neural Network to predict the number of cases of COVID-19, and it's quite accurate.
tags: [AI, python, covid-19]
readtime: true
cover-img: /assets/img/rona.jpg
image: /assets/img/AI.png
comments: true
---

## Introduction
So I made a Deep Neural Network to predict the number of cases of COVID-19, and it's quite accurate.
Proof?
See For yourself: 
![Prediction Graph](https://cdn.discordapp.com/attachments/709095218535858198/730028120333352990/wMQL5Zme1b6QAAAABJRU5ErkJggg.png)
Cool right?

So, How exactly is this possible? Is this that accurate? Was the prediction made with appropriate settings?
The short answer is :

> "When something looks too good to be true, it usually is." 

### How does this work

Let me walk you through an example of building a [Long Short Term Memory (LSTM)](https://en.wikipedia.org/wiki/Long_short-term_memory) neural network to predict the number of cases that gives the prediction results you saw above.

LSTMs are a type of [Recurrent Neural Networks (RNN)](http://karpathy.github.io/2015/05/21/rnn-effectiveness/) 's Which are used for time-series problems. They are often used in predicting cryptocurrency prices, stock market prices, etc.

If you don't want to know how the code works and wanna get to the code: [Here is the GitHub Repo](https://github.com/EliteDaMyth/COVID-Predictor).

So, We first read the `COVID-CASES.csv` file & tell panda that the index is `Date` Column:
```py
hist = pd.read_csv('COVID-CASES.csv')
hist = hist.set_index('Date')
```
 then, we use `hist.head()` to show the first 5 rows to make sure everything is working.
 
 ![hist.head()](https://cdn.discordapp.com/attachments/655302848849903646/730038384377987072/unknown.png)

Now, We split the data into two parts.

 - Training data,
 - Testing data.
 
 90% of the data is used  for training while the last 10% is used for testing our prediction
 ![training/testing](https://cdn.discordapp.com/attachments/655302848849903646/730039172483645541/A15qqTzbP9SHgUuA06hmCr2nqb6WeFbgCLmnqXjv51aSpOkoUkptxyBJkiRJ0sPsUZUkSZIkDRUTVUmSJEnSUDFRlSRJkiQNFRNV.png)
*The above image says Prediction data but I meant testing data :P*

Now, we build the Training model for the LSTM.
I won't detail this part, if you want to see the source go [Here](https://github.com/EliteDaMyth/COVID-Predictor/blob/master/lstm_covid_prediction.ipynb) and scroll down to the LSTM part.

I used a simple neural network with a single LSTM layer consisting of  `20`  neurons, a dropout factor of  `0.25`.
I trained the network for  `50`  epochs with a batch size of  `2`.

Using the trained model to predict the test set, we obtain the graph shown in the beginning.

![Prediction Graph](https://cdn.discordapp.com/attachments/709095218535858198/730028120333352990/wMQL5Zme1b6QAAAABJRU5ErkJggg.png)

So what exactly is happening here? Why does this look so accurate?

So, If you have gone through the code, You might have seen the flaw already. 

The flaw with this model is that _for the prediction of a particular day, it mostly uses the value of the previous day._

The prediction line is not much more than a shifted version of the actual price.

If we adjust the Prediction line to be one day back, It will *almost* entirely overlap the Actual Data line.


### Last Words

Sadly, The data cannot be *accurately* predicted by any AI. The above AI is just predicting the data for the next day while looking at the current day's cases. 

**You should not use this as any sort of medical advice, etc.
This project is just a PoC and to educate people.**

Thanks, 
To contact me to talk about this, Contact me through discord: EliteDaMyth#0690 ;)
