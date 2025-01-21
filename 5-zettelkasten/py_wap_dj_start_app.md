### Meta
2025-01-21 11:22
**Tags:** [[py_projects]] [[py_web_app]] [[py_wap_django]]
**Status:** #pending 

### Starting an App
A Django *project* is organized as a group of individual *apps* that work together to make the project work as a whole.

Leave the development server running in the terminal window. In another window (or tab), navigate to the directory that contains *manage.py*. Activate the virtual environment and run the `startapp` command.
```BASH title:example.sh
source ll_env/bin/activate
python manage.py startapp learning_logs
ls
ls learning_logs/
```

The command `startapp appname` tells Django to create the infrastructure needed to build an app. Looking into the `learning_logs` directory, the most important files are *models.py*, *admin.py*, and *views.py*. We’ll use *models.py* to define the data we want to manage in our app.

##### Defining Models
Each user will need to create a number of topics in their learning log. Each entry they make will be tied to a topic, and these entries will be displayed as text. We’ll also need to store the timestamp of each entry so we can show users when they made each one.

Open the file *models.py* and look at its existing content:
```Python title:models.py
from django.db import models

# Create your models here.
```

A module called `models` is being imported, and we’re being invited to create models of our own. A *model* tells Django how to work with the data that will be stored in the app. A model is a class; it has attributes and methods, just like every class we’ve discussed. Here’s the model for the topics users will store:
```Python title:models.py
from django.db import models

class Topic(models.Model):
	"""A topic the user is learning about."""
	text = models.CharField(max_length=200)
	date_added = models.DateTimeField(auto_now_add=True)

	def __str__(self):
		"""Return a string representation of the model."""
		return self.text
```

We’ve created a class called `Topic`, which inherits from `Model`–a parent class included in Django that defines the model’s basic functionality. We add to attributes to the `Topic` class: `text` and `date_added`.

The `text` attribute is a `CharField`, a piece of data that’s made up of characters or text. You use `CharField` when you want to store a small amount of text, such as a name, a title, or a city. When we define a `CharField` attribute, we have to tell Django how much space it should reserve in the database. Here we give it a `max_length` of `200` characters, which should be enough to hold most topic names.

The `date_added` attribute is a `DateTimeField`, a piece of data that will record a date and time. We pas the argument `auto_now_add=True`, which tells Django to automatically set this attribute to the current date and time whenever the user creates a new topic.

It’s a good idea to tell Django how you want to represent an instance of a model. If a model has a `__str__()` method, Django calls that method whenever it needs to generate output referring to an instance of that model. Here we’ve written a `__str__()` method that returns the value assigned to the `text` attribute.

##### Activating Models
1234