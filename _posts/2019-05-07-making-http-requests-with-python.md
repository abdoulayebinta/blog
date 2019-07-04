---
layout: post
title:  "Making HTTP Request with Python!"
author: abdoulaye
categories: [development , data science]
tags: [red, yellow]
image: assets/images/python-RestAPI.png
description: "My review of Inception movie. Acting, plot and something else in this short description."
featured: false
hidden: false
rating: 4.5
---
How can we request data from an API.
Send an **HTTP** request, get data back and parse it as **JSON**

## HTTP Introduction 
- Describe what happens when you type a URL in the URL bar
- Describe the request/response cycle
- Explain what request or response header is, and give examples
- Explain the different categories of response codes
- Compare **GET** and **POST** requests
 
What happens when...
1. DNS Lookup
2. Computer makes a REQUEST to a server
3. Server processes the REQUEST
4. Server issues a RESPONSE

2,3 and 4 are called the Request/Response cycle

HTTP Headers 

- Sent with both requests and responses
- Provide additional information about the request or response

### Header Examples
**Request Headers**
- **Accept** - Acceptable content-types for response (e.g html, json, xml)
- **Cache-Control** - Specify caching behavior 
- **User-Agent** - Information about the software used to 
make the request


## Response Status Codes
- 2xx - Success
- 3xx - Redirect
- 4xx - Client Error (your fault!)
- 5xx - Server Error (not your fault!)


# HTTP Verbs and APIs

## HTTP Verbs

**GET**
- Useful for retrieving data
- Data passed in query string
- Should have no "side-effects"
- Can be cached
- Can be bookmarked

**POST**
- Useful for writing data
- Data passed in request body 
- Can have side-effects
- Not cached
- Can't be bookmarked


## APIs
- **API**   - Application Programming Interface
- Allows you to get data from another application without
needing to understand how the application works
- Can often send data back in different formats
- Examples of companies with APIs: GitHub, Spotify, Google


## Writting our first Python Request

Using the _requests_ Modules

- Lets us make HTTP requests from our Python code!
- Install **requests** using pip 
- Useful for web scrapping/crawling, grabbing data from other APIs, etc

```bash
python3 -m pip install requests
```

```python
import requests

# Making a GET request to Hacker News
response = request.get("https://news.ycombinator.com/")
print(response) # <Response [200]>
print(response.ok) # True

# If we look at the response's headers
# we can see somthing like this
print(response.headers)
# {'Server': 'nginx', 'Date': 'Tue, 28 May 2019 13:21:27 GMT', 'Content-Type': 'text/html; charset=utf-8', 'Transfer-Encoding': 'chunked', 'Connection': 'keep-alive', 'Vary': 'Accept-Encoding', 'Cache-Control': 'private; max-age=0', 'X-Frame-Options': 'DENY', 'X-Content-Type-Options': 'nosniff', 'X-XSS-Protection': '1; mode=block', 'Referrer-Policy': 'origin', 'Strict-Transport-Security': 'max-age=31556900', 'Content-Security-Policy': "default-src 'self'; script-src 'self' 'unsafe-inline' https://www.google.com/recaptcha/ https://www.gstatic.com/recaptcha/ https://cdnjs.cloudflare.com/; frame-src 'self' https://www.google.com/recaptcha/; style-src 'self' 'unsafe-inline'", 'Content-Encoding': 'gzip'}
```

Make a GET requests to google.com

```python 
import requests

url = "http://www.google.com"
response = requests.get(url)

print(f"your request to {url} came back with status code {response.status_code}")
```

## Requesting JSON with Python 

```python
import requests

url = "https://icanhazdadjoke.com/"
# Get the response in JSON format
response = requests.get(url, headers={"Accept": "application/json"})

# turn the response into python code, from string to python dictionary
data = response.json()

print(data["joke"])
print(f"status: {data['status']}")
```

## Sending Requests with Params

### What's a Query String?

- A way to pass data to the server as part of a GET request
- http://www.example.com/?_key1=value1&key2=value2_


Query String 

```python 
# Option 1

import requests

response = requests.get("http://www.example.com/?key1=value1&key2=value2")
```
```python 
# Option 2 - preferable!

import requests

response = requests.get(
    "http://www.example.com",
    params={
        "key1": "value1",
        "key2": "value2"
    })
```
Examples of query string.
Searching for a joke using the search endpoint: https://icanhazdadjoke.com/search

```python
import requests

url = "https://icanhazdadjoke.com/search"
# Get the response in JSON format and specify the query string as params
response = requests.get(
    url, 
    headers={"Accept": "application/json"},
    params={"term": "cat", "limit": 1})

# turn the response into python code, from string to python dictionary
data = response.json()
print(data["results"])
```



