# Notes 🐍

-   [Libraries and Modules](#libraries-and-modules)
    -   [Modules](#modules)
    -   [External libraries](#external-libraries)
-   [Practical Applications](#practical-applications)
    -   [Working with Files](#working-with-files)
-   [Using Python](#using-python)
    -   [`main` Method](#main-method)
    -   [Debugging](#debugging)
    -   [Testing](#testing)
-   [Object Oriented Python](#object-oriented-python)
-   [Exceptions](#exceptions)
    -   [`try-except`](#try-except)
-   [Web Frameworks](#web-frameworks)
-   [APIs](#apis)
    -   [HTTP Methods](#http-methods)
    -   [Headers, Body and Parameters](#headers-body-and-parameters)
    -   [Response Types](#response-types)
    -   [HTTP status Codes](#http-status-codes)
    -   [`requests` + APIs](#requests--apis)
    -   [Practice: GitHub stars](#practice-github-stars)

## Libraries and Modules

### Modules

-   We can import external libraries and also our own code, modules, using `import`.
-

#### pretty print

Pretty print is a module included in the Python standard library that prettify prints.

```py
>>> long_list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]
>>> long_list
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]
>>> from pprint import pprint
>>> pprint(long_list)
[0,
 1,
 2,
 3,
 4,
 5,
 6,
 7,
 8,
 9,
 10,
 11,
 12,
 13,
 14,
 15,
 16,
 17,
 18,
 19,
 20,
 21,
 22,
 23]
```

### External libraries

-   `pip install requests` will install that external library. Then we can import it with `import`: `import requests`

## Practical Applications

### Working with Files

Python provides a built-in function for opening files, cleverly titled open(). The open() method will return an object that you can read() to get the data. By default, open() will open a file in read-only mode, however you can change this by passing a mode parameter. The list of optional modes is here:

| Character | Meaning                                                         |
| --------- | --------------------------------------------------------------- |
| ‘r’       | open for reading (default)                                      |
| ‘w’       | open for writing, truncating the file first                     |
| ‘x’       | open for exclusive creation, failing if the file already exists |
| ‘a’       | open for writing, appending to the end of the file if it exists |
| ‘b’       | binary mode                                                     |
| ’t’       | text mode (default)                                             |
| ’+’       | open a disk file for updating (reading and writing)             |

## Using Python

### `main` Method

Let's say we have a file named `name_lib.py` and another one called `other_program.py`

name_lib.py

```py
def upper_case_name(name):
    return name.upper()

name = "Nina"
name_upper = upper_case_name(name)
print(f"Upper case name is {name_upper}")
```

other_program.py

```py
import name_lib

my_name = "Fred"
upper_name = name_lib.upper_case_name(my_name)

print(f"In my own code, upper name is {upper_name}")
```

We we run this code, this will print first "Upper case name is NINA" and then "In my own code, upper name is FRED". But imagine that's a problem for us, that if we run the second file, we only want to see its own code, and not the one with "Nina". We should use the main method.

If we edit name_lib.py to this, adding `print("dunder name", __name__)` at the end...

```py
def upper_case_name(name):
    return name.upper()

name = "Nina"
name_upper = upper_case_name(name)
print(f"Upper case name is {name_upper}")

print("dunder name", __name__)
# Sometimes dunder is how __ is called in Python
```

... we'll see that the last line will be printed as "`dunder name __main__`". Instead, if we run the code from the other file, it will print `dunder name name_lib`, and of course all the naming stuff.

Now we know this, we could insert a conditional statement in the first file:

```py
def upper_case_name(name):
    return name.upper()

if __name__ = "__main__":
    name = "Nina"
    name_upper = upper_case_name(name)
    print(f"Upper case name is {name_upper}")
    print("dunder name", __name__)
```

Now if we run `other_program.py` it just will say that my name is Fred.

### Debugging

-   We can insert some `print()` statements in the middle of the code.

### Testing

## Object Oriented Python

## Exceptions

### `try-except`

-   Python we'll try to run the code under `try` and if that's impossible, it will run the code inside of `except` instead of returning a exception.

```py
int("a")
print("hello")
```

This will be problematic, so we say:

```py
try:
    int("a")
except:
    print("there may be an error")
print("hello")
```

If we still want to know more about what could happen in the `try` block we could add `ValueError as e`. `e` is just a way to name an exception and call it later.

```py
try:
    int("a")
except ValueError as e:
    print("there may be an error: ", e)
print("hello")

# there may be an error: invalid literal for int() with base 10: 'a'
# hello
```

## Web Frameworks

## APIs

-   Set of functions or procedures that allow accessing features or data of a system somewhere else.
-   Might require authentication or no.
-   Client → (send request to) → Server → (return response to) → Client

### HTTP Methods

The HTTP Method (or verb) is how you tell the server which _type_ of operation you'd like to perform.

-   `GET`: Ask the server to get a resource.
-   `POST`: Ask the server to create a resource, with the data that you've provided.
-   `PUT`: Edit or update a resource.
-   `DELETE`: Delete a resource.

### Headers, Body and Parameters

-   We can add additional to our request through headers, a body or URL parameters.
-   Example of URL parameter: `https://exame.com?var1=foo&var2=bar`.

### Response Types

-   XML was more popular in the past, now JSON is the more common format.
-   JSON is a common format of capturing data, and it's easy to read and generate from a variety of programming languages.

### HTTP status Codes

-   This code is a numerical response from the server, indicating the status of the request. They tend to fall into these categories:
-   `1xx`: Informational.
    -   Not commonly used.
-   `2xx`: Success.
    -   `200 OK`: Standard response for successful HTTP requests.
    -   `201 CREATED`: A new resource was created successfully.
-   `3xx`: Redirection
    -   `301 Moved Permanently`: This and all future requests should be directed to the new URL.
-   `4xx`: A Client Error
    -   `404 Not Found`: An entry wasn't found based on the information the client gave.
-   `5xx`: A Server Error
    -   `500 Internal Server Error`: Something went wrong with the server.

### `requests` + APIs

-   Let's use the `requests` library to interact with APIs.

```py
# First thing we'll do is import the requests library
import requests

# Define a variable with the URL of the API
api_url = "http://shibe.online/api/shibes?count=1"

# Call the root of the api with GET, store the answer in a response variable
# This call will return a list of URLs that represent dog pictures
response = requests.get(api_url)

# Get the status code for the response. Should be 200 OK
# Which means everything worked as expected
print(f"Response status code is: {response.status_code}")
# An alternative to {response.status_code} may be to declare a variable status_code = response.status_code

# Get the result as JSON
response_json = response.json()

# Print it. We should see a list with one image URL.
print(response_json)

```

```response
(env) $ python shibe.py
Response status code is: 200
['https://cdn.shibe.online/shibes/28d7c372ea7defdb315ef845285d4ac3906ccea4.jpg']
```

We could also stablish how many responses we want using parameters. In this case, we'll say that we want 10 urls of dogs.

```py
# We'll store our base URL here and pass in the count parameter later
api_url = "http://shibe.online/api/shibes"

params = {
   "count": 10
}

# Pass those params in with the request.
api_response = requests.get(api_url, params=params)

print(f"Shibe API Response Status Code is: {api_response.status_code}")  # should be 200 OK

json_data = api_response.json()

print("Here is a list of URLs for dog pictures:")
for url in json_data:
    print(f"\t {url}")
```

```response
shibe.py
Shibe API Response Status Code is: 200
Here is a list of URLs for dog pictures:
     https://cdn.shibe.online/shibes/dfb2af0b2ac1f057750da32f0ea0e154afc160cf.jpg
     https://cdn.shibe.online/shibes/4989daad2c805ec62b0fb09a80280ba2262f1b08.jpg
     https://cdn.shibe.online/shibes/a9360b8262c586af2cf53a2d68bb6ec34b87fe25.jpg
     https://cdn.shibe.online/shibes/a168cc7f2524c73b433afd7c02f698884738daff.jpg
     https://cdn.shibe.online/shibes/3fbe49908948718c521b756f31dc155ed22941f6.jpg
     https://cdn.shibe.online/shibes/846bb52389cf9af8a54eb12f48e0e7d0883b17da.jpg
     https://cdn.shibe.online/shibes/d11ed7f57c5a882f047b921a73f0b95714626bb3.jpg
     https://cdn.shibe.online/shibes/0fd1dcc9f5866cefaa3040de1be0f8971b0530cd.jpg
     https://cdn.shibe.online/shibes/cd668ca05d0ec78863f3c30b08b9cd4ff7f5669c.jpg
     https://cdn.shibe.online/shibes/32bf0797e5a4c5bfb6fc06edc57ddfbf4e08f98f.jpg
```

### Practice: GitHub stars

```py
"""
A small Python program that uses the GitHub search API to list
the top projects by language, based on stars.

GitHub Search API documentation: https://developer.github.com/v3/search/

Additional parameters for searching repos can be found here:
https://help.github.com/en/articles/searching-for-repositories#search-by-number-of-stars

Note: The API will return results found before a timeout occurs,
so results may not be the same across requests, even with the same query.

Requests to this endpoint are rate limited to 10 requests per
minute per IP address.
"""

import requests


def create_query(languages, min_stars=50000):
    """
    Create the query string for the GitHub search API,
    based on the minimum amount of stars for a project, and
    the provided programming languages.

    An example search query looks like:
    stars:>50000 language:python language:javascript
    """
    query = f"stars:>{min_stars} "

    for language in languages:
        query += f"language:{language} "

    return query


def repos_with_most_stars(languages, sort="stars", order="desc"):
    gh_api_repo_search_url = "https://api.github.com/search/repositories"
    query = create_query(languages)

    # Define the parameters we want to be part of our URL
    parameters = {"q": query, "sort": sort, "order": order}

    # Pass in the query and the parameters as part of the request.
    response = requests.get(gh_api_repo_search_url, params=parameters)
    status_code = response.status_code

    # Check if the rate limit was hit. Applies only for students running this code
    # in the in-person course.
    if status_code == 403:
        raise RuntimeError("Rate limit reached. Please wait a minute and try again.")
    if status_code != 200:
        raise RuntimeError(f"An error occurred. HTTP Status Code was: {status_code}.")
    else:
        response_json = response.json()
        records = response_json["items"]
        return records


if __name__ == "__main__":
    languages = ["python", "javascript", "ruby"]
    results = repos_with_most_stars(languages)

    for result in results:
        language = result["language"]
        stars = result["stargazers_count"]
        name = result["name"]

        print(f"-> {name} is a {language} repo with {stars} stars.")

```
