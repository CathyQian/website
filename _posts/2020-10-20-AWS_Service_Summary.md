---
layout: post
title: AWS Service Summary
description: A short summary of AWS services used widely by data scientists.
date: 2020-10-20
tags: data science, machine learning, AWS, software engineering
comments_id: 21
---

Cloud-based solution for 
- data storage
- computing (or data processing)

They are all scalable because they are distributed solutions.

- S3
It is an object store for **data storage**.

- Sagemaker
It is a **computing** platform used specifically for machine learning. You can use SageMaker Jupyter Notebook, model deployment via endpoint, save or import data to or from S3.

- EC2 (Elastic Compute Cloud)
Amazon Elastic Compute Cloud (Amazon EC2) is a web service that provides secure, resizable **computing** platform in the cloud. It is designed to make web-scale cloud computing easier for developers. 

- EMR
EMR is a **computing** platform for **big data processing**. It spins up a cluster in the cloud so that you can use open source tools such as Apache Spark, Apache Hive, Apache HBase, Apache Flink, Apache Hudi, and Presto to query and process data and save both input and output files into AWS S3.

**EMR is a collection of EC2 instances with Hadoop (and optionally Hive and/or Pig) installed and configured on them**. If you are using your cluster for running Hadoop/Hive/Pig jobs, EMR is the way to go. An EMR instance costs a little bit extra as compared to an EC2 instance.

Reference: https://www.youtube.com/watch?v=jylp2atrZjc