### Meta
2025-01-24 19:48
**Tags:** [[py_projects]] [[py_web_app]] [[py_wap_django]]
**Status:** #completed 

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
Next, we must create a page that can focus on a single topic, showing the topic name and all the entries for that topic. We’ll define a new URL pattern, write a view, and create a template. We’ll also modify the topics page so each item in the bulleted list links to its corresponding topic page.

##### The Topic URL Pattern
The URL pattern for the topic page is a little different from the prior URL patterns because it will use the topic’s `id` attribute to indicate which topic was requested. For example, if the user wants to see the detail page for the Chess topic (where the `id` is `1`), the URL will be `http://localhost:8000/topics/1`. Here’s a pattern to match this URL, which you should place in `learning_logs/urls.py`:
```Python title:learning_logs/urls.py
--snip--
urlpatterns = [
	--snip--
	# Detail page for a single topic.
	path('topics/<int:topic_id>', views.topic, name='topic'),
]
```

The first part of the string tells Django to look for URLs that have the word *topics* after the base URL. The second part of the string, `/<int:topic_id>`, matches an integer between two forward slashes and assigns the integer value to an argument called `topic_id`.

When Django finds a URL that matches this pattern, it calls the view function `topic()` with the value assigned to `topic_id` as an argument. We’ll use the value of `topic_id` to get the correct topic inside the function.

##### The Topic View
The `topic()` function needs to get the topic and all associated entries from the database, much like what we did earlier in the Django shell:
```Python title:views.py
--snip--
def topic(request, topic_id):
	"""Show a single topic and all its entries."""
	topic = Topic.objects.get(id=topic_id)
	entries = topic.entry_set.order_by('-date_added')
	context = {'topic': topic, 'entries': entries}
	return render(request, 'learning_logs/topic.html', context)
```

This is the first view function that requires a parameter other than the `request` object. The function accepts the value captured by the expression `/<int:topic_id>/` and assigns it to `topic_id`. Then we use `get()` to retrieve the topic, just as we did in the Django shell. Next, we get all of the entries associated with this topic and order them according to `date_added`. The minus sign in front of `date_added` sorts the results in reverse order, which will display the most recent entries first. We store the topic and entries in the `contex` dictionary and call `render()` with the `request` object, the *topic.html* template, and the `context` dictionary.

**Note:** The code phrases on lines 4 and 5 are called *queries*, because they query the database for specific information. When you’re writing queries like these in your own projects, it’s helpful to try them out in the Django shell first. You’ll get much quicker feedback in the shell than you would by writing a view and template and then checking the results in a browser.

##### The Topic Template
The template must display the name of the topic and the entries. We must also inform the user if no entries have been made yet for this topic.
```HTML title:topic.html
{% extends 'learning_logs/base.html' %}

{% block content %}
	<p>Topic: {{ topic. text }}</p>

	<p>Entries:</p>
	<ul>
		{% for entry in entries %}
			<li>
				<p>{{ entry.date_added|date:'M d, Y H:i' }}</p>
				<p>{{ entry.text|linebreaks }}</p>
			</li>
		{% empty %}
			<li>There are no entries for this topic yet.</li>
	</ul>
	
{% endblock content %}
```

##### Links from the Topics Page
Before we look at the topic page in a browser, we must modify the topics template so each topic links to the appropriate page.
```HTML title:topics.html
--snip--
	{% for topic in topics %}
		<li>
			<a href="{% url 'learning_logs:topic' topic.id %}">{{ topic.text }}</a>
		</li>
	{% empty %}
--snip--
```

**Note:** There’s a subtle but important difference between `topic.id` and `topic_id`. The expression `topic.id` examines a topic and retrieves the value of the corresponding ID. The variable `topic_id` is a reference to that ID in the code.