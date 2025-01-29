### Meta
2025-01-25 14:02
**Tags:** [[py_projects]] [[py_web_app]] [[py_wap_user_accounts]]
**Status:** #pending 

### Allowing a User to Enter Data
Before we build an authentication system for creating accounts, we’ll first add some pages that allow users to enter their own data. We’ll give users the ability to add a new topic, add a new entry, and edit their previous entries.

Currently, only a superuser can enter data through the admin site. We don’t want users to interact with the admin site, so we’ll use Django’s form-building tools to build pages that allow users to enter data.

#### Adding New Topics
We’ll start by allowing users to add a new topic. Adding a form-based page works in much the same way as adding the pages we’ve already built: we define a URL, write a view function, and write a template. The one significant difference is the addition of a new module called *forms.py*, which will contain the forms.

##### The Topic ModelForm
Any page that lets a user enter and submit information on a web page involves an HTML element called a *form*. When users enter information, we need to *validate* that the information provided is the right kind of data and is not malicious, such as code designed to interrupt our server. We then need to process and save valid information to the appropriate place in the database. Django automates much of this work.

The simplest way to build a form in Django is to use a `ModelForm`. Write your first form in the file *forms.py*, which should be created in the same directory as *models.py*:
```Python title:forms.py
from django import forms

from .models import Topic

class TopicForm(forms.ModelForm):
	class Meta:
		model = Topic
		fields = ['text']
		labels = {'text': ''}
```

The simplest version of a `ModelForm` consists of a nested `Meta` class telling Django which model to base the form on and which fields to include in the form. Here we specify that the form should be based on the `Topic` model, and that it should only include the `text` field. The empty string in the labels dictionary tells Django not to generate a label for the `text` field.

##### The new_topic URL
The URL for a new page should be short and descriptive. When the user wants to add a new topic, we’ll send them to `http://localhost:8000/new_topic/`.
```Python title:learning_logs/urls.py
--snip--
urlpatterns = [
	--snip--
	# Page for adding a new topic.
	path('new_topic/', views.new_topic, name='new_topic'),
]
```

##### The new_topic() View Function
The `new_topic()` function needs to handle two different situations: initial requests for the `new_topic` page, in which case it should show a blank form; and the processing of any data submitted in the form. After data from a submitted form is processed, it needs to redirect the user back to the `topics` page:
```Python title:views.py
from django.shortcuts import render, redirect

from .models import Topic
from .forms import TopicForm

--snip--
def new_topic(request):
	"""Add a new topic."""
	if request.method != 'POST':
		# No data submitted; create a blank form.
		form = TopicForm()
	else:
		# POST data submitted; process data.
		form = TopicForm(data=request.POST)
		if form.is_valid():
			form.save()
			return reditrect('learning_logs:topics')

	# Display a blank or invalid form.
	context = {'form': form}
	return render(request, 'learning_logs/new_topic.html', context)
```

test

test 2

test3
