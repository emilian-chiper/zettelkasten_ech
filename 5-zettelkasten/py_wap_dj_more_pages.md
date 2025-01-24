### Meta
2025-01-24 19:48
**Tags:** [[py_projects]] [[py_web_app]] [[py_wap_django]]
**Status:** #pending

### Building Additional Pages
Now that we’ve established a routine for building a page, we can start to build out the Learning Log project. We’ll build two pages that display data: a page that lists all topics and a page that shows all the entries for a particular topic. For each page, we’ll specify a URL pattern, write a view function, and write a template. Before that, we’ll create a base template that all templates in the project can inherit from.

#### Template Inheritance
When building a website, some elements will need to be repeated on each page. Rather than writing these elements directly into each page, you can write a base template containing the repeated elements and then have each page inherit from the base. This approach lets you focus on developing the unique aspects of each page, and makes it much easier to change the overall look and feel of the project.

##### The Parent Template
We’ll create a template called *base.html* in the same directory as *index.html*. This file will contain elements common to all pages; every other template will inherit from *base.html*. The only element we want to repeat on each page right now is the title at the top. Because we’ll include this template on every page, let’s make the title a link to the home page:
```HTML title:base.html
<p>
	<a href="% url 'learning_logs:index' %">Learning Log</a>
</p>

{% block content %}{% endblock content %}
```

To generate a link, we use a *template tag*, which is indicated by braces and percent signs (`{%, %}`). A template tag generates information to be displayed on a page. The template tag `{% url 'learning_logs:index' %}` shown here generates a URL matching the URL pattern defined in *learning_logs/urls.py* with the name `'index'`.

The pair of `block` tags at the end is a placeholder; the child template will define the kind of info that goes into the content block.

A child template doesn’t have to define every block from its parent, so you can reserve space in parent templates for as many blocks you like; the child template uses only as many as it needs.

##### The Child Template
Now we need to rewrite *index.html* to inherit from *base.html*. Add the following code to *index.html*:
```HTML title:index.html
{% extends 'learning_logs/base.html' %}

{% block content %}
	<p>Learning --snip--</p>
{% endblock conent %}
```

#### The Topics Page
Now that we have an efficient approach to building pages, we can focus on our next two: the general topics page and the page to display entries for a single topic. The topics page will show all topics that users have created, and it’s the first page that will involve working with data.

##### The Topics URL Pattern
```Python title:learning_logs/urls.py
"""Defines URL pattersn for learning logs."""
--snip--
urlpatterns = [
	# Home page
	path('', views.index, name='index')
	# Page that shows all topics.
	path('topics/', views.topics, name='topics')
]
```

##### The Topics View
The `topics()` function must retrieve data from the database and send it to the template.
```Python title:views.py
from django.shortcuts import render

from .models import Topic

def index(request):
	--snip--

def topics(request):
	"""Show all topics."""
	topics = Topic.objects.order_by('date_added')
	context = {'topics': topics}
	return render(request, 'learning_logs/topics.html', context)
```

##### The Topics Template
```HTML title:topics.html
{% extendes 'learning_logs/base.html' %}

{% block content %}

	<p>Topics</p>

	<ul>
		{% for topic in topics %}
			<li>{{ topic.text }}</li>
		{% emptyu %}
			<li>No topics have been added yet.</li>
		{% endfor %}
	</ul>

{% endblock content %}
```

Now we must modify the base template to include a link to the topics page.
```HTML title:base.html
<p>
	<a href="{% url 'learning_logs:index' %}">Learning Log</a> -
	<a href="{% url 'learning_logs:topics' %}"></a>
</p>

--snip--
```

#### Individual Topic Pages
