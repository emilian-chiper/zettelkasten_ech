### Meta
2025-01-20 08:12
**Tags:** [[python]] [[py_projects]] [[py_data_visualization]]
**Status:** #completed 

### Working With APIs
We’ll write a self-contained program that generates a visualization based on data it retrieves. We’ll use an API to automatically request specific information from a website and then use that info to generate a visualization. Because programs written like this always use current data to generate a visualization, even when the data might be rapidly changing, the visualization will always be up to date.

#### Using an API
An *application programming interface* (API) is a part of a website designed to interact with programs.  Those programs use very specific URLs to request certain information. This kind of request is called an *API call*. The requested data will be returned in an easily processed format, such as JSON or CSV. Most apps that use external data resources, such as apps that integrate with social media sites, rely on API calls.

##### Git and GitHub
We’ll base our visualization on information from GitHub’s API to request info about Python projects on the site, and then generate an interactive visualization of the relative popularity of these projects using Plotly.

##### Requesting Data Using an API Call
GitHub’s API lets you request a wide range of information through API calls.
```HTTP title:api_call
https://api.github.com/search/repositories?q=language:python+sort:stars
```

This call returns the number of Python projects currently hosted on GitHub, as well as info about the most popular Python repos. Let’s examine it. The first part, `http://api.github.com/`, directs the request to the part of GitHub that responds to API calls. The next part, `search/repositories`, tells the API to conduct a search through all the repositories on GitHub.

The question mark after `repositories` signals that we’re about to pass an argument. The `q` signals that we’re about to pass an argument. The `q` stands for *query*, and the equal sign `=` lets us begin specifying a query. By using `language:python`, we indicate that we want information only on repositories that have Python as the primary language. The final part, `+sort:stars`, sorts the projects by the number of stars they’ve been given.

The following snippet shows the first few lines of the response:
```JSON title:response.json
{
  "total_count": 8961993,
  "incomplete_results": true,
  "items": [
	{
      "id": 54346799,
      "node_id": "MDEwOlJlcG9zaXRvcnk1NDM0Njc5OQ==",
      "name": "public-apis",
      "full_name": "public-apis/public-apis",
      --snip--
```

You can see from the response that this URL isn’t primarily intendef to be entered by humans, because it’s in a format that’s meant to be processed by a program. GitHub found just under nine million Python projects as of this writing. The value for `"incomplete_results"` is `true`, which tells us that Github didn’t fully process the query. GitHub limits how long each query can run, as to keep the API responsive for all users. In this case, it found some of the most popular Python repositories, but it didn’t have time to find all of them; we’ll address that shortly. The `"items"` returned are displayed in the list that follows, which contains details about the most popular Python projects on GitHub.

##### Installing Requests
The *Request* package allows a Python program to easily request information from a website and examine the response.
```BASH title:install_requests.sh
python -m pip install --user requests

# On linux, inside a virtual environment:
pip install requests
```

##### Processing an API Response
Now we’ll write a program to automatically issue an API call and process the results:
```Python title:python_repos.py
import requests

# Make an API call and check the response.
url = "https://api.github.com/search/repositories"
url += "?q=language:python+sort:start+stars:>10000"

headers = {"Accept": "application/vnd.github.v3+json"}
r = requests.get(url, headers=headers)
print(f"Status code: {r.status_code}")

# Convert the response object to a dictionary.
response_dict = r.json()

# Process results.
print(response_dict.keys())
```

We first import the `requests` module, then assign the URL of the API call to the `url` variable. This is a long URL, so we break it into two lines: the first line is the main part of the URL, and the second line is the query string. We’ve included one more condition to the original query string: `stars:>10000`, which tells GitHub to only look for python repositories that have more than 10,000 stars. This should allow GitHub to return a complete, consistent set of results.

GitHub is currently on the third version of its API, so we define headers for the API call that ask explicitly to use this version of the API, and return the results in the JSON format. Then we use `requests` to make the call to the API. We call `get()` and pass it the URL and the header that we defined, and we assign the response object to the variable `r`.

The response object has an attribute called `status_code`, which tells us whether the request was successful. A status code of `200` indicates a successful response. We print the value of `status_code` so we can make sure the call went through successfully. We asked the API return the information in JSON format, so we use the `json()` method to convert the information to a Python dictionary. We assign the resulting dictionary to `response_dict`.

Finally, we print the keys from `response_dict` and see the following output:
```BASH title:output.sh
Status code: 200
dict_keys(['total_count', 'incomplete_results', 'items'])
```

Because the status code is `200`, we know that the request was successful. The response dictionary contains only three keys:  `total_count`, `incomplete_results`, and `items`. Let’s take a look inside the response dictionary.

##### Working with the Response Dictionary
With the information from the API call represented as a dictionary, we can work with the data stored there. Let’s generate some output that summarizes the information. This is a good way to make sure we received the information we expected, and to start examining the information we’re interested in:
```Python title:python_repos.py
import requests

# Make an API call and store the response.
--snip--

# Convert the response object to a dictionary.
response_dict = r.json()
print(f"Total repositories: {response_dict['total_count']}")
print(f"Complete results: {not response_dict['incomplete_results']}")

# Explore information about the repositories.
repo_dicts = response_dict['items']
print(f"Repositories returned: {len(repo_dicts)}")

# Examine the first repository.
repo_dict = repo_dicts[0]
print(f"\nKeys: {len(repo_dict)}")
for key in sorted(repo_dict.keys()):
	print(key)
```

The results give us a clearer picture of the actual data:
```BASH title:output.sh
Status code: 200
Total repositories: 4044
Complete results: True
Repositories returned: 30

Keys: 80
allow_forking
archive_url
archived
--snip--
url
visibility
watchers
watchers_count
web_commit_signoff-required
```

Let’s pull out the values for some of the keys in `repo_dict`:
```Python title:python_repos.py
--snip--
# Examine the first repository.
repo_dict = repo_dicts[0]

print("\nSelected informatin about first repository:")
print(f"Name: {repo_dict['name']}")
print(f"Owner: {repo_dict['owner']['login']}")
print(f"Stars: {repo_dict['stargazers_count']}")
print(f"Repository: {repo_dict['html_url']}")
print(f"Created: {repo_dict['created_at']}")
print(f"Updated: {repo_dict['updated-at']}")
print(f"Description: {repo_dict['description']}")

"""
Status code: 200
Total repositories: 4044
Complete results: True
Repositories returned: 30

Selected information about first repository:
Name: freeCodeCamp
Owner: freeCodeCamp
Stars: 409034
Repository: https://github.com/freeCodeCamp/freeCodeCamp
Created: 2014-12-24T17:49:19Z
Updated: 2025-01-20T09:41:27Z
Description: freeCodeCamp.org's open-source codebase and curriculum. Learn to code for free.
"""
```

##### Summarizing the Top Repositories
When we make a visualization for this data, we’ll want to include more than one repository. We’ll write a loop to print selected information about each repository the API call returns so we can include them all in the visualization:
```Python title:python_repos.py
--snip--
# Explroe information about the repositories.
repo_dicts = response_dict['items']

print("\nSelected information about each repository:")
for repo_dict in repo_dicts:
	print(f"\nName: {repo_dict['name']}")
	print(f"Owner: {repo_dict['owner']['login']}")
	print(f"Stard: {repo_dict['stargazers_count']}")
	print(f"Repository: {repo_dict['html_url']}")
	print(f"Description: {repo_dict['description']}")

"""
Status code: 200
Total repositories: 248
Complete results: True
Repositories returned: 30
Selected information about each repository:
Name: public-apis
Owner: public-apis
Stars: 191494
Repository: https://github.com/public-apis/public-apis
Description: A collective list of free APIs
Name: system-design-primer
Owner: donnemartin
Stars: 179952
Repository: https://github.com/donnemartin/system-design-primer
Description: Learn how to design large-scale systems. Prep for the system
design interview. Includes Anki flashcards.
--snip--
Name: PayloadsAllTheThings
Owner: swisskyrepo
Stars: 37227
Repository: https://github.com/swisskyrepo/PayloadsAllTheThings
Description: A list of useful payloads and bypass for Web Application Security
and Pentest/CTF
"""
```

##### Monitoring API Rate Limits
Most APIs have *rate limits*, which means there’s a limit to how many requests you can make in a certain amount of time. To see if you’re approaching GitHub’s limits, enter `https://api.github.com/rate-limit` into a web browser. The response should begin like this:
```JSON title:response.json
{
  "resources": {
    --snip--
    "search": {
      "limit": 10,
      "remaining": 9,
      "reset": 1652338832,
      "used": 1,
      "resource": "search"
    },
    --snip--
```

**Note:** Many APIs require you to register and obtain an API key or access token to make API calls. As of this writing, GitHub has no such requirements, but if you obtain an access token, your limits will be much higher.

#### Visualizing Repositories Using Plotly
We’ll make an interactive bar chart: the height of each bar will represent the number of stars the project has acquired, and you’ll be able to click the bar’s label to go to that project’s home on GitHub.
```Python title:python_repos_visual.py
import requests
import plotly.express as px

# Make an API call and check the response.
url = "https://api.github.com/search/repositories"
url += "?q=language:python+sort:stars+stars:>10000"

headers = {"Accept": "application/vnd.github.v3+json"}
print(f"Status code: {r.status_code}")

# Process overall results.
response_dict = r.json()
print(f"Complete results: {not response_dict['incomplete_results']}")

# Process repository information.
repo_dicts = response_dict['items']
repo_names, stars = [], []
for repo_dict in repo_dicts:
	repo_names.append(repo_dict['name'])
	stars.append(repo_dict['stargazers_count'])

# Make visualization.
fig = px.bar(x=repo_names, y=stars)
fig.show()
```

##### Styling the Chart
We’ll make some changes in the initial `px.bar()` call and then make some further adjustments to the `fig` object after it’s been created.
```Python title:python_repos_visual.py
# Make visualization.
title = "Most-Starred Python Projects on GitHub"
labels = {'x': 'Repository', 'y': 'Stars'}
fig = px.bar(x=repo_names, y=stars, title=title, labels=labels)

fig.update_layout(title_font_size=28, xaxis_title_font_size=20, yaxis_title_font_size=20)

fig.show()
```

##### Adding Custom Tooltips
In Plotly, you can hover the cursor over an individual bar to show the information the bar represents. This is commonly called a *tooltip*, and in this case, it currently shows the number of stars a project has. We must pool some additional data to generate the tooltips:
```Python title:python_repos_visual.py
--snip--
# Process repository information.
repo_dicts = response_dict['items']
repo_names, stars, hover_texts = [], [], []
for repo_dict in repo_dicts:
	repo_names.append(repo_dict['name'])
	stars.append(repo_dict['stargazers_count'])

	# Build hover texts.
	owner = repo_dict['owner']['login']
	description = repo_dict['description']
	hover_text = f"{owner}<br />{description}"
	hover_texts.append(hover_text)

# Make visualization.
title = "Most-Starred Python Projects on GitHub"
labels = px.bar(x=repo_names, y=stars, title=title, labels=labels, hover_name=hover_texts)

fig.update_layout(title_font_size=28, xaxis_title_font_size=20, yaxis_title_font_size=20)

fig.show()
```

##### Adding Clickable Links
Because Plotly allows you to use HTML on text elements, we can easily add links to a chart. Let’s use the *x*-axis label as a way to let the viewer visit any project’s home page on GitHub. We must pull the URLs from the data and use them when generating the *x*-axis labels:
```Python title:python_repos_visual.py
--snip--
# Process repository information.
repo_dicts = response_dict['items']
repo_links, stars, hover_texts = [], [], []
for repo_dict in repo_dicts:
	# Turn repo names into active links.
	repo_name = repo_dict['name']
	repo_url = repo_dict['html_url']
	repo_link = f"<a href='{repo_url}'>{repo_name}</a>"
	repo_links.append(repo_link)

	stars.append(repo_dict['stargazers_count'])
	--snip--

# Make visualization.
title = "Most-Starred Python Projects on GitHub"
labels = {'x': 'Repository', 'y': 'Stars'}
fig = px.bar(x=repo_links, y=stars, title=title, labels=labels, hover_name=hover_texts)

--snip--
```

##### Customizing Marker Colors
Once a chart has been created, almost any aspect of the chart can be customized through an update method. We’ve used `update_layout()` previously. Another method, `update_traces()`, can be used to customize the data that’s represented on a chart.

Let’s change the bars to a darker blue, with some transparency:
```Python title:python_repos_visual.py
--snip--
fig.update_layout(title_font_size=28, xaxis_font_size=20, yaxis_font_size=20)

fig.update_traces(marker_color='SteelBlue', marker_opacity=0.6)

fig.show()
```

In Ploty, a *trace* refers to a collection of data on a chart. The `update_traces()` method can take a number of different arguments; any argument that starts with `marker_affects` the markers on the chart. Here we set each marker’s color to `SteelBlue`; any named CSS color will work here. We also set the opacity of each marker to `0.6`. An opacity of `1.0` would be entirely opaque.

#### The Hacker News API
The following call returns information about the current top article as of this writing:
```HTTP title:example
https://hacker-news.firebaseio.com/v0/item/31353677.json
```

When you enter this URL in a browser, you’ll see that the text on the page is enclosed by braces, meaning it’s dictionary. But the response is difficult to examine without some better formatting. We’ll run this URL through `json.dumps()` method, so we can explore the kind of information returned about an article:
```Python title:hn_article.py
import requests
import json

# Make an API call, and store the response.
url = "https://hacker-news.firebaseio.com/v0/item/31353677.json"
r = requests.get(url)
print(f"Status code: {r.status_code}")

# Explore the structure of the data.
response_dict = r.json()
response_string = json.dumps(response_dict, indent=4)
print(response_string)

"""
{
	"by": "sohkamyung",
	"descendats": 307,
	"id": 31353677,
	"kids": [
        31354987,
        31354235,
        31354040,
		--snip--
	],
	"score": 786,
	"time": 1652361401,
	"title": "Astronomers reveal first image of black hole at the heart of our galaxy",
	"type": "story",
	"url": "https://public.nrao.edu/news/astronomers-reveal-first-image-of-the-black-hole-at-the-heart-of-our-galaxy/"
}
"""
```

We can use this call to fin out which articles are on the home page right now, and then generate a series of API calls similar to the one we just examined. With this approach, we can print a summary of all the articles on the front page of Hacker News at the moment:
```Python title:hn_submissions.py
from operator import itemgetter

import requests

# Make an API call and check the response.
url = "https://hacker-news.firebase.io.com/v0/topstories.json"
r = requests.get(url)
print(f"Status code: {r.status_code}")

# Process information about each submission.
submission_ids = r.json()
submission_dicts = []
for submission_id in submission_ids[:5]:
	# Make a new API call for each submission.
	url = f"https://hacker-news.firebaseio.com/v0/item/{submission_id}.json"
	r = requests.get(url)
	print(f"id: {submission_id}\tstatus: {r.status_code}")
	response_dict = r.json()

	# Build a dictionary for each article.
	submission_dict = {
		'title': response_dict['title']
		'hn_link': f"https://news.ycombinator.com/item?id={submission_id}",
		'comments': response_dict['descendants'],
	}
	submission_dicts.append(submission_dict)

submission_dicts = sorted(submission_dicts, key=itemgetter('comments'), reverse=True)

for submission_dict in submission_dicts:
	print(f"\nTitle: {submission_dict['title']}")
	print(f"Discussion link: {submission_dict['hn_link']}")
	print(f"Comments: {submission_dict['comments']}")

"""
Status code: 200
id: 42768072    status: 200
id: 42769871    status: 200
id: 42766825    status: 200
--snip--

Title: DeepSeek-R1
Discussion link: https://news.ycombinator.com/item?id=42768072
Comments: 136

Title: Celestial Navigation for Drones
Discussion link: https://news.ycombinator.com/item?id=42767797
Comments: 34

Title: Zork: The Great Inner Workings (2020)
Discussion link: https://news.ycombinator.com/item?id=42767132
Comments: 4
--snip--
"""
```