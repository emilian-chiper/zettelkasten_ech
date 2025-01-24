### Meta
2025-01-24 18:50
**Tags:** [[py_projects]] [[py_web_app]] [[py_wap_django]]
**Status:** #completed 

### Making Pages: The Learning Log Home Page
Making web pages with Django consists of three stages: defining URLs, writing views, and writing templates. You can do these in any order, but in this project we’ll always start by defining the URL pattern. A *URL pattern*  describes the way the URL is laid out. It also tells Django what to look for when matching a browser request with a site URL, so it knows which page to return.

Each URL then maps to a particular view. The *view* function retrieves and processes the data needed for that page. The view function often renders the page using a *template*, which contains the overall structure of the page. To see how this works, let’s make the home page for Learning Log. We’ll define the URL for the home page, write its view function, and create a simple template.

Because we just want to ensure the Learning Log works as if it’s supposed to, we’ll make a simple page for now. A functioning web app is fun to style when completed; an app that looks good but doesn’t work well is pointless. For now, the home page will display only a title and a brief description.

#### Mapping a URL
Users request pages by entering URLs into a browser and clicking links, so we’ll need to decide what URLs are needed. The home page URL is first: it’s the base URL people use to access the project. At the moment, the base URL, `http://localhost:8000`, returns the default Django site that lets us know the project was set up correctly. We’ll change it by mapping the base URL to Learning Log’s home page.

In the main *ll_project* directory, open the file *urls.py*. Change it to look like so:
```Python title:ll_project/urls.py
from django.contrib import admin
from djago.urls import path, include

urlpattenrs = [
	path('admin/', admin.site.urls),
	path('', include('learning_logs.urls'))
]
```

The default *urls.py* is in the *ll_project* folder; now we must make a second urls.py file in the *learning_logs* folder.
```Python title:learning_logs.py
"""Defines URL patterns for learning_logs."""

from django.urls import path

from .import views

app_name = 'learning_logs'
urlpatterns = [
	# Home page
	path('', views.index, name='index')
]
```

The actual URL patterns is a call to the `path()` function, which takes three arguments. The first argument is a string that helps Django route the current request properly. Django receives the requested URL and tries to route the request to a view. It does this by searching all the URL patterns we’ve defined to find one that matches the current request. Django ignores the base URL for the project (`http://localhost:8000`), so the empty string matches the base URL. Any other URL won’t match this pattern, and Django will return an error page if the URL requested doesn’t match any existing URL patterns.

The second argument in `path()` specifies which function to call in *views.py*. When a requested URL matches the pattern we’re defining, Django calls the `index()` function from *views.py*. The third argument provides the name *index* for this URL pattern so we can refer to it more easily in other files throughout the project. Whenever we want to provide a link to the home page, we’ll use this name instead of writing out a URL.

##### Writing a View
A view function takes in information from a request, prepares the data needed to generate a page, and then sends the data back to the browser. It often does this by using a template that defines what the page will look like.

The file *views.py* in *learning_logs* was generated automatically when we ran the command `python mange.py startapp`. Make it look like this:
```Python title:views.py
from django.shortcuts import render

def index(request):
	"""The home page for Learning Log."""
	return render(request, 'learning_logs/index.html')
```

When a URL request matches the pattern we just defined, Django looks for a function called `index()` in the *views.py* file. Django then passes the `request` object to this view function. In this case, we don’t need to process any data for the page, so the only code in the function is a call to `render()`. The `render()` function here passes two arguments: the original `request` object and a template it can use to build the page.

##### Writing a Template
The template defines what the page should look like, and Django fills in the relevant data each time the page is requested. A template allows you to access any data provided by the view. Because our view for the home page provides no data, this template is fairly simple.

Inside the *learning_logs* folder, make a new folder called *templates*. Inside *templates*, make another folder called *learning_logs*. This might seem redundant, but it sets up a structure that Django can interpret unambiguously, even in the context of a large project containing many individual apps. Inside the inner *learning_logs* folder, make a new file called *index.html*. The path to the file will be `ll_project/learning_logs/templates/learning_logs/index.html`. Fill it with one each of a header and paragraph elements.