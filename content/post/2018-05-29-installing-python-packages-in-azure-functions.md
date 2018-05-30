---
title: Installing Python packages in Azure Functions
author: Lucas A. Meyer
date: '2018-05-29'
slug: installing-python-packages-in-azure-functions
categories:
  - Data Science
  - Python
tags:
  - Data Science
  - Python
header:
  caption: ''
  image: ''
---

### A few tricks when using Python in Azure Functions

#### Installing a more recent version of Python for your Azure Functions

The Python version in Azure Functions is pretty old. As of this writing (May 2018), it's still on version 2.7. Let's install version 3.5.

1. Open the [Azure Portal](https://portal.azure.com)

2. Select your function App (usually under App Services)

3. Select "Platform Features" on top

![Platform Features](/img/python-platform.png)

4. Select "Advanced Tools (Kudu)"

![Select Kudu](/img/python-kudu1.png)

5. Select "CMD" on the "Debug Console"

![Debug Console -> CMD](/img/python-kudu.png)


