# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Project 3: Web APIs & NLP

### Problem Statement

We want to distinguish between those who are **willfully wrong** about history from those who are merely **uninformed**. Those in the former category are more dangerous, as since they present themselves as correct more people will follow their misinformation. The two categories can be analyzed by using the Pushshift API to take posts from two subreddits, **r/badhistory** and **r/AskHistorians**.

The point of this exercise is to determine which classification model can correctly predict which posts come from which subreddit. The final model should be used by media companies (including Reddit itself) who want to combat misinformation by showing which words are associated with actively false and misleading claims.


### Overview

**r/badhistory** is a subreddit dedicated to rebuttals of books and other writings which present false or misleading claims about history. Most posts consist almost exclusively of direct quoting from the cited material, and the actual rebuttals only take up a few lines. No questions are allowed.

**r/AskHistorians** is a subreddit entirely devoted to academic-level questions about history. Its main rule is that there are no questions about history within the last 20 years.

I took over 1000 posts from each subreddit using the Pushshift API. After splitting each post up into words, taking out the most common words in each subreddit, and lemmatizing the remaining words, I used three models on the data and compared them:
1. **Multinomial Naive Bayes**, which calculates the probability that a post with given words is in a particular subreddit using Bayes's theorem.
2. **Logistic Regression**, which calculates the log probability of a post being in a subreddit using a function on several linear variables.
3. **Random Forest Classification**, which splits the data into several decision trees and then classifies the data based on which subset it is in.

Since the point of this problem is to correctly identify those who are **wrong** about history, it was more important that I have better specificity (more correct "0" - r/badhistory) than sensitivity (more correct "1" - r/AskHistorians) in my model.


### Sources

* Pushshift API for r/badhistory: *https://api.pushshift.io/reddit/search/submission?subreddit=badhistory*
* Pushshift API for r/AskHistorians: *https://api.pushshift.io/reddit/search/submission?subreddit=askhistorians*


### Conclusions & Further Research

Given both its high specificity (0.82) and accuracy (0.824), I would argue to use the **random forest classifier** model to determine whether a post is in r/AskHistorians or r/badhistory based on its contents.

As r/badhistory contains so many posts with links (since many of the most common words in its posts are associated with links), future research would need to show if an algorithm can clearly tell non-link posts in r/badhistory from those in r/AskHistorians.