---
title: Yo, Stroop!
author: Lucas A. Meyer
date: '2018-08-23'
slug: yo-stroopwafel
categories:
  - Bots
tags:
  - Bots
header:
  caption: ''
  image: ''
---

YoStroop is a bot that allows members of a slack channel to give rewards to each other, usually as a way of saying "thank you" for help and valuable contributions. 
It was developed using Python, Azure Functions v2.0 and Cosmos DB.


## Motivation

One of the Data Science Slack channels I'm a member of tried several different tools to keep track of the valuable contributions of its members. Some of the tools that we used to to track contributions became quite expensive and we started looking for an alternative. Since most people in the channel can program in R and Python, I thought we might develop our own Slack bot. I wanted to create a Slack bot that was:

1. Written in a language that most Data Scientists are familiar with (e.g. Python or R)
2. Virtually free to run
3. Serverles
4. Used very well known technologies (e.g., `pyodbc` for databases)
5. Easy to maintain and deploy from GitHub with no hassle

I have failed to achieve almost all of the goals above, but the future looks more promising.

## Architecture