---
layout: post
title: The Right Way to Refresh Machine Learning Models
description: Summary of metrics to consider when retraining machine learning models
date: 2020-12-09
tags: machine learning, modeling, retrain
comments_id: 25
---

Machine learning models get stale quickly as data or pattern shift (namely covariate shift and concept shift/model drift) so that relationships in old data can no longer make good predictions in new data and thus need to be retrained. 

- When to retrain?
Once you trained your model, you have a measure of accuracy.

You should retrain your model when the accuracy drops below a certain threshold. This can be delayed as you probably won't have the ground truth for a while


--> monitoring data drift (model monitoring dashboard), can also be hard to tell

--> scheduled retrain (weekly, monthly, quarterly)

--> an extreme case: online learning (update the data as new data come in)

The other senario to retrain the model is when new data is available

- How to retrain?
quick updates: only change the data, model params the same
more comprehensive: change both the data and the model

--> continual learning (incorporate real-time data in production, fully automated) (how? retrain all the model? too slow)

Rather retraining simply refers to re-running the process that generated the previously selected model on a new training set of data. The features, model algorithm, and hyperparameter search space should all remain the same. One way to think about this is that retraining doesn’t involve any code changes. It only involves changing the training data set.
such changes would ideally be introduced with A/B tests that measure the impact of the new model on predetermined metrics of interest such as user engagement or retention.

How often should you retrain your model? 
It depends.In a more dynamic environment such as fraud detection or online advertising --- online learning where the model is updated incrementally as new data becomes available
mannual retraining (periodic or upon a trigger)

And how do you determine your new training set?
Typically this uses a sliding window approach, e.g. remove the oldest day from the training set, and add in the new day of data. Then retrain your model, evaluate its performance and if it really does perform better against current conditions, deploy it. Alternatively, the new model can be retrained with a combination of data for the old model and new data, if performance improves.


automatically monitor the performance of your model in production on new data and determine if it is suddenly under-performing

- How to compare old and new model? For both regression and classification problems
- To use the retrained model or not?
what tools to use?
Kubernetes

# References
1. https://mlinproduction.com/model-retraining/
2. https://nanonets.com/blog/machine-learning-production-retraining/#questions-to-ask-before-retraining


