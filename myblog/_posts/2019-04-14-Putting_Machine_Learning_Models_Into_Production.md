---
layout: post
title: Putting Machine Learning Models Into Production
date: 2019-04-14
---

# Putting Machine Learning Models Into Production

**This is a collection of notes copied directly or indirectly from reference 1.**

The deployment of machine learning models is the process for making your models available in production environments, where they can provide predictions to other software systems. It is only once models are deployed to production that they start adding value, making deployment a crucial step. 

**Why hard?**

Machine learning systems have all the challenges of traditional code, plus an additional set of machine learning-specific issues. 

- The need for reproducibility

    Particularly in industries under the scrutiny of regulatory authorities, the ability to reproduce predictions made by models means that the quality of software logs, dependency management, versioning, data collection and feature engineering pipelines and many other areas has to be extremely high.

- Change anything changes everything  

    Feature engineering and selection changes must be easily tracked; data and configurations may also change and needs to be tracked.

- Data and Feature Preparation

    If left unchecked, vast webs of of scripts, joins, scrapes and intermediate output files can form around various steps of data munging and feature engineering. Unpicking or maintaining such “glue code” is a deeply frustrating and error-prone task for even an experienced software developer.

- Error

    Many things can go wrong -- wrong version of model, forgetting a feature, training on an outdated dataset etc.

- Separation of Expertise (business, data science, software engineering, devops)
    
    Machine learning systems require cooperation between multiple teams, which can result in no single team or person understanding how the overall system works, teams blaming each other for failures, and general inefficiencies.

Machine learning system design needs to be planned at a system level instead of isolated model deployment. Initial deployment is not that hard, the hardest part is the ongoing system maintenance, the updates and experiments, the auditing and monitoring that are where the real technical debts starts to build up.

## Machine Learning System Architecture

Start with business requirements and wider company goals:
- Do you need to be able to serve predictions in real time (and if so, do you mean like, within a dozen milliseconds or after a second or two), or will delivery of predictions 30 minutes or a day after the input data is received suffice?
- How often do you expect to update your models?
- What will the demand for predictions be (i.e. traffic)?
- What size of data are you dealing with?
- What sort(s) of algorithms do you expect to use (and do you really need them)
- Are you in a regulated environment where the ability to audit your system is important?
- Does your company have product-market fit? (i.e. do you need to prepare for the system’s original purpose to radically change)
- Can this task be done without ML?
- How large and experienced is your team - including data scientists, engineers and DevOps?

Here is a summary of some technical keypoints:
- Streaming (Typically such designs rely on a distributed streaming platform such as Apache Kafka) is much harder than batch transformation. Prediciton result delivery can be via REST API or through shared database (PUPPY, high latency), which makes it easy to manage the ML system.

- The common programming language used is python, as life is way easier if the language you use in the research environment matches your production environment; however, if speed is a real concern, then python may not be feasible; only switch language when necessary.

- Build for reproducibility from the start: Persist all model inputs and outputs, as well as all relevant metadata such as config, dependencies, geography, timezones and anything else you think you might need if you ever had to explain a prediction from the past. Pay attention to versioning, including of your training data.
    
- Treat your ML steps as part of your build: Which is to say, automate training and model publishing.
    
- Plan for extensibility: If you are likely to be updating your models on a regular basis, you need to think carefully about how you will do this from the beginning.
    
- Modularity: To the largest extent possible, aim to reuse preprocessing and feature engineering code from the research environment in the production environment.
    
- Testing: Plan to spend significantly more time on testing your machine learning applications.

- Use reproducible pipelines (i.e., scikit-learn or mleap pipelines)

- Use containers: Bottom line: Build your machine learning system so that all parts of it (including model training, testing and serving) can be containerized.

- Kubernetes — do I need it?

    Kubernetes has become very popular, but it doesn’t mean you have to use it from day one. If you are a small startup and your immediate aim is to develop a minimum product, Kubernetes can wait. However, if you already need to scale, use microservice orchestration, and you have some experience with Kubernetes, you should not postpone its adoption.

- Use CI/CD (continuous integration / continuous deployment) tool (i.e., Jenkens, GitLab) to allowing delivering code changes more frequently and reliably. If you use Kubernetes as an orchestrator you should consider GitLab for CI/CD. It natively supports Kubernetes and works with multiple clusters.

## Deployment strategy:
- Shadow mode: Version B receives real-world traffic alongside version A while doesn’t impact the response.
- Canary deployments: Version B is released to a subset of users, then proceed to a full rollout.

## Test
Traditional software test such as unit test, integration test and system test should be done. In addition, the following tests specific to machine learning systems should also be included:
- **Differential Tests**: Where you compare the average/per row predictions given by a new model vs. the predictions given by the old model on a standard **test dataset**. You need to tweak the sensitivity of these tests depending on the model use case. These tests can be vital for detecting otherwise healthy-seeming models, for example where an outdated dataset has been used in training, or a feature has been accidentally removed from the feature selection code. 
- **Benchmark Tests**: These tests compare the time taken to either train or serve predictions from your model from one version to the next. They prevent you from introducing inefficient code additions to your ML applications.
- **Load/Stress tests**: These are not really ML-specific, but given the unusually large CPU/Memory demands of some ML applications, these sorts of tests are particularly worth performing.

## Deployment
Don't try and reinvent the wheel, using established software engineering practices instead.

Many companies have their own platform:
- Uber’s platform is called Michelangelo
- Facebook has FBLearner Flow
- Google has TFX
- Databricks have MLFlow

## Trend

Kubeflow aims to simplify machine learning on Kubernetes. It’s still relatively new, with all the risks that entails, but it will enable smaller teams with less DevOps expertise to do complex container orchestration for machine learning tasks.

The growth of serverless solutions, with the usual suspects weighing in (Azure Functions, Google Cloud Functions, AWS Lambda), combined with on-demand ML APIs from the same players.

More ways to bridge the gap between the research and production environment, for example at Netflix they have invested significant effort into being able to use Jupyter notebooks for production tasks.
    
More companies creating solutions focused on the issues discussed in this post - data labeling and versioning, model automated testing, validation and lifecycle management.
    
Client-side machine learning with TensorFlow.js. This is still very bleeding edge, and it’s not clear to me how comfortable companies will be allowing all their model code to be readable by the competition.
    
Growth of so called “real time” ML systems, where models are updated constantly as new data streams come in. This is in part helped by the established position Apache Kafka has now created, but there are interesting alternatives gaining traction such as Apache Pulsar.


References:
1. https://christophergs.com/machine%20learning/2019/03/17/how-to-deploy-machine-learning-models/#architecture

2. https://papers.nips.cc/paper/5656-hidden-technical-debt-in-machine-learning-systems.pdf

3. https://christophergs.com/machine%20learning/2020/03/14/how-to-monitor-machine-learning-models/

4. https://martinfowler.com/articles/cd4ml.html

5. https://landing.google.com/sre/sre-book/chapters/testing-reliability/
