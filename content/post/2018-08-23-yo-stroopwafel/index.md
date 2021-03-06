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

[YoStroop](https://github.com/RealLucasMeyer/yostroop) is a bot that allows members of a slack channel to give rewards to each other, usually as a way of saying "thank you" for help and valuable contributions. 
It was developed using Python, Azure Functions v2.0 and Cosmos DB.


## Motivation

One of the Data Science Slack channels I'm a member of tried several different tools to keep track of the valuable contributions of its members. Some of the tools that we used to to track contributions became quite expensive and we started looking for an alternative. Since most people in the channel can program in R and Python, I thought we might develop our own Slack bot. Developing a Slack Bot is really straightforward. You essentially need a HTTP server that will receive JSONs and call Web APIs. I wanted to create a Slack bot that was:

1. Written in a language that most Data Scientists are familiar with (e.g. Python or R)
2. Virtually free to run
3. Serverless
4. Based on very well known technologies (e.g., `pyodbc` for databases)
5. Easy to modify from GitHub with no hassle
6. Developed and maintained in any major platform: Windows, macOS or Linux

I have failed to achieve almost all of the goals above, but maybe will achieve most in the near future.

## Azure Functions v2

Microsoft recently released a [Python worker](https://github.com/Azure/azure-functions-python-worker) for the 
[Azure Functions runtime v2](https://docs.microsoft.com/en-us/azure/azure-functions/functions-versions). 
As of this writing (2018-08-23), both Azure Functions v2 and the python worker are in "preview mode". The Azure Functions v1 runtime supports development and hosting only in the portal or on Windows. The v2 runtime runs on .NET Core, and therefore can run on Windows, macOS and Linux. Microsoft provides a 
[set of tools](https://github.com/Azure/azure-functions-core-tools) based on Node.JS and .NET Core that make it easy to develop in any platform. That takes care of objectives #1, #3 and #6. Although knocking off three objectives simply by selecting Azure Functions v2 sounded very promising to begin with, that's as many objectives as I could achieve.

### Linux host

Regardless of the platform you develop on, Python function apps need to be hosted on 
[Azure Functions on Linux](https://blogs.msdn.microsoft.com/appserviceteam/2017/11/15/functions-on-linux-preview/). Running on Linux has a couple downsides:

1. You have to access the Azure Portal using a 
[secret code](https://ms.portal.azure.com/?websitesextension_pythonFunctions=true) to enable Azure to offer Linux hosts

2. As of this writing (2018-08-23), Linux hosts can only be dedicated. Azure Functions can normally run in two modes: "Consumption" and "Dedicated". Consumption is virtually free, but the "dedicated" mode costs approximately $35 per month for the cheapest version. According to the [README](https://github.com/Azure/azure-functions-python-worker/blob/dev/README.md) the "Consumption" mode is upcoming, and I have a small allowance due to my MSDN subscription, so I caved.

And there goes objective #2. But it seems temporary, so we're probably good.

### Developing a Slack Bot

A Slack bot is essentially an HTTP server that will receive JSONs and perform actions through HTTP requests. Azure Functions have an HTTP Trigger template, so this takes care of most of the plumbing. I created a Slack app using the instructions [here](https://api.slack.com/bot-users). This bot subscribes to events, which are sent to an URL. I've created the HTTP Server that provides that URL using the instructions on [how to create a function using the command line interface](https://github.com/Azure/azure-functions-python-worker/wiki/Create-Function-(CLI)), and creating a [sample based on the HttpTrigger](https://github.com/Azure/azure-functions-python-worker/tree/dev/tests/http_functions).

Specifically, my Azure Function receives JSONs for each message, parses them to see if they have a `:stroopwafel:`, and if they do, parses the mentions (@user) in the message. For each mention, we log a :stroopwafel: gift in a database, from which we can build reports at the end of a period.

### PyODBC 

The original idea was tha whenever a message mentioned a `:stroopwafel:`, the bot would use `pyodbc` to save the message in a database. Databases are usually not free, but Azure offers SQL Server for as low as $5 per month, and that seemed acceptable. The problem is that `pyodbc` does not have a linux wheel, and currently Azure Functions for Linux [requires wheels](https://github.com/Azure/azure-functions-core-tools/issues/640). There's a way of compiling the package on the fly, but it currently has a bug. And I don't know how long it will take to fix that bug.

I searched for alternatives to PyODBC, and the best alternative was to use [Cosmos DB](https://docs.microsoft.com/en-us/azure/cosmos-db/introduction), since its Python package `pydocumentdb` has a wheel. The downside is that the cheapest Cosmos DB plan as of this writing costs $25. And now we're far away from objective #2, and we're also not doing great with objective #4. However, I found Cosmos DB a pleasure to use.

### GitHub

Once I was done with my development, which [Azure Functions Core Tools](https://github.com/Azure/azure-functions-core-tools) made really convenient by setting a local test server whenever I run `func host start`, I pushed [my repository to GitHub](https://github.com/RealLucasMeyer/yostroop) and configured the Azure Function app to consume it using Continuous Deployment, which is something that you can set up in Azure with just a few clicks. However, [it doesn't yet work](https://github.com/Azure/azure-functions-core-tools/issues/640) (sad trombone). Luckily, deploying without GitHub is not that bad. Again, Azure Functions Core Tools provides a command-line interface utility that pushes your application to the server: `func azure functionapp publish <app-name>`, and you're done in a couple of minutes. But I also don't fulfill objective #5.

## Verdict

Although I was so far unable to fulfill half of my initial objectives, it looks like I'll get there soon. There's something magical about Azure Functions. It does a lot of the hard work for you, and if you're familiar with one of the many languages available, you can deploy your program to production really fast. I had never developed a Slack bot before, and I've started the bot during a sleepless night and finished it in an afternoon. All in, it took me less than two days of work to get an app to production. There are still some kinks to be worked out but Azure Functions v2 has already proved to be useful to me.

I wrote about Azure Functions before, specifically about [using Python in Azure Functions v1](https://meyerperin.com/post/installing-python-packages-in-azure-functions/). Azure Functions can be very useful for Data Scientists: it's an easy way to deploy a model to production, perform scheduled maintenance, update datasets on a schedule, etc. With v2, Python became a first class player. I'm sure I'll use it a lot.

