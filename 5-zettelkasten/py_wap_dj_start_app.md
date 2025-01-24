### Meta
2025-01-21 11:22
**Tags:** [[py_projects]] [[py_web_app]] [[py_wap_django]]
**Status:** #completed 

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
To use our models, we must tell Django to include our app in the overall project. Open *settings.py* (in the *ll_project* directory); you’ll see a section that tells Django which apps are installed in the project:
```Python title:settings.py
--snip--
INSTALLED_APPS = [
	'django.contrib.admin',
	'django.contrib.auth',
	'django.contrib.contenttypes',
	'django.contrib.sessions',
	'django.contrib.messages',
	'django.contrib.staticfiles',
]
--snip--
```

Add our app to the list by modifying `INSTALLED_APPS` so it looks like this:
```Python title:settings.py
--snip--
INSTALLED_APPS = [
	# My apps.
	'learning_logs',
	# Default django apps.
	'django.contrib.admin',
	--snip--
]
--snip--
```

Next, we must tell Django to modify the database so it can store information related to the model `Topic`. From terminal, run the following command:
```BASH title:example.sh
python manage.py makemigrations learning_logs
```

The command `makemigrations` tells Django to figure out how to modify the database so it can store the data associated with any new models we’ve defined. The output here shows that Django has created a migration file called *001_initial.py*. This migration will create a table for the model `Topic` in the database.

Now we’ll apply this migration and have Django modify the database for us:
```BASH title:example.sh
python3 manage.py migrate
```

Most of the output from this command is identical to the output from the first time we issued the `migrate` command. We must check the last line in this output, where Django confirms that the migration for `learning_logs` worked `OK`.

Whenever we want to modify the data that Learning Log manages, we’ll follow these three steps:
- modify *models.py*,
- call `makemigrations` on `learning_logs`, and
- tell Django to `migrate` the project.

##### The Django Admin Site
Django makes it easy to work with your models through its admin site. Django’s *admin site* is only meant to be used by the site’s administrators; it’s not meant for regular users. In this section, we’ll set up the admin site and use it to add some topics through the `Topic` model.

###### Setting Up a Superuser
Django allows you to create a *superuser*, a user who has all privileges available on the site. A user’s *privilege* control the actions they can take. The most restrictive privilege settings allow a user to only read public information on the site. Registered users typically have the privilege of reading their own private data and some selected information available only to members. To effectively administer a project, the site owner usually needs access to all information stored on the site. A good administrator is careful with their user’s sensitive information, because users put a lot of trust into the apps they access.

To create a superuser in Django, enter the following command and respond to prompts:
```BASH title:example.sh
python manage.py createsuperuser
Username: ll_admin
Email address:
Password:
Password (again):
Superuser created successfully.
```

**Note:** Some sensitive information can be hidden from a site’s administrators. For example, Django doesn’t store the password you enter; instead, it stores a string derived from the password, called a `hash`. Each time you enter your password, Django hashes your entry and compares it to the stored hash. If the two hashes match, you’re authenticated. By requiring hashes to match, Django ensures that if an attacked gains access to the site’s database, they’ll be able to read the stored hashes but not the passwords. When a site is set up properly, it’s almost impossible to get the original passwords from the hashes.

###### Register a Model with the Admin Site
Django includes some models in the admin site automatically, such as `User` and `Group`, but the models we create need to be added manually.

When we started the `learning_logs` app, Django created an *admin.py* file in the same directory as *models.py*. Open the *admin.py* file:
```Python title:admin.py
from django.contrib import admin

# Register your models here.
```

To register `Topic` with the admin site, enter the following:
```Python title:admin.py
from django contrib import admin

from .models import Topic

admin.site.register(Topic)
```

This code first imports the model we want to register, `Topic`. The dot in front of `models` tells Django to look for *models.py* in the same directory as *admin.py*. The code `admin.site.register()` tells Django to manage our model through the admin site.

Now you can use the superuser account to access the admin site. Go to `https://localhost:8000/admin/` and enter the username and password for the super-user you just created.

**Note:** If you see a message in your browser that the web page is not available, ensure you still have the Django server running in a terminal window. If you don’t, activate a virtual environment and reissue the command `python manage.py runserver`. If you’re having trouble viewing your project at any point in the development process, closing any open terminals and reissuing the `runserver` command is a good first troubleshooting step.

###### Adding Topics
Now that `Topic` has been registered with the admin site, let’s add our first topic. Click **Topics** to go to the Topics page, which is mostly empty, because we have no topics to manage yet. Click **Add Topic**, and a form for adding a new topic appears. Enter `Chess` in the first box and click **Save**. You’ll be sent back to the Topics admin page, and you’ll see the topic you just created.

We’ll create a second topic so we have more data to work with. Let’s go for `Rock Climbing`.

##### Defining the Entry Model
For a user to record what they’ve been learning about chess and rock climbing, we must define a model for the kinds of entries users can make in their learning logs. Each entry must be associated with a particular topic. This relationship is called *many-to-one*, meaning many entries can be associated with one topic.

Here’s the code for the entry mdoel:
```Python title:models.py
from django.db import models

class Topic(models.Model):
	--snip--

class Entry(models.Model):
	"""Something specific learned about a topic."""
	topic = models.ForeignKey(Topic, on_delete=models.CASCADE)
	text = models.TextField()
	date_added = models.DateTimeField(auto_now_add=True)

	class Meta:
		verbose_name_plural = 'entries'

	def __str__(self):
		"""Return a simple string representing an entry."""
		return f"{self.text[:50]}..."
```

The `Entry` class inherits from Django’s base `Model` class, just as `Topic` did. The first attribute, `topic`, is a `ForeignKey` instance. A *foreign key* is a database term; it’s a reference to another record in the database. This is the code that connects each entry to a specific topic. Each topic is assigned a *key*, or ID, when created. When Django must establish a connection between two pieces of data, it uses the keys associated with each piece of information. We’ll use these connections shortly to retrieve all the entries associated with a certain topic. The `on_delete=modes.CASCADE` argument tells Django that when a topic is deleted, all the entries associated with that topic should be deleted as well. This is known as a *cascading delete*.

Next is an attribute called `tex`, which is an instance of `TextField`. This kind of field doesn’t need a size limit, because we don’t want to limit the size of individual entries. The `date_added` attribute allows us to present entries in the order they were created, and to place a timestamp next to each entry.

The `Meta` class is nested inside the `Etnry` class. The `Meta` class holds extra info for managing a model; here, it lets us set a special attribute telling Django to use `Entries` when it must refer to more than one entry. Without this, Django would refer to multiple entries as `Entrys`.

The `__str__()` method tells Django which information to show when it refers to individual entries. Because an entry can be a long body of text, `__str__()` returns just the first `50` characters of `text`. We also add an ellipsis to clarify that we’re not always displaying the entire entry.

##### Migrating the Entry Model
Because we’ve added a new model, we must migrate the database again.
```BASH title:example.sh
python manage.py makemigrations learning_logs
python manage.py migrate
```

##### Registering Entry with the Admin Site
```Python title:admin.py
from django.contrib import admin

from .models import Topic, Entry

admin.site.register(Topic)
admin.site.register(Entry)
```

Go back to `http://localhost/admin/`, and you should see Entries listed under *Learning_Logs*. Click the **Add** link for Entries, or click **Entries** and then choose **Add entry**. You should see a drop-down list to select the topic you’re creating an entry for and a text box for adding an entry. Select **Chess** from the drop-down list, and add an entry, something like:
`The opening is the first part of the game, roughly the first ten moves or so. In the opening, it's a good idea to do three things--bring out your bishops and knights, try to control the center of the board, and castle your king.`
`Of course, these are just guidelines. It will be important to learn when to follow these guidelines and when to disregard these suggestions.`

When you click **Save**, you’ll be brought back to the main admin page for entries. Here, you’ll see the benefit of using `text[:50]` as the string representation of each entry; it’s much easier to work with multiple entries in the admin interface if you see only the first part of an entry, rather than the entire text of each entry.

Make a second entry for Chess and one entry for Rock Climbing so we have some initial data. Here’s a second entry for Chess:
`In the opening phase of the game, it's important to bring out your bishops and knights. These pieces are powerful and maneuverable enough to play a significant role in the beginning moves of a game.`

And here’s a first entry for Rock Climbing:
`One of the most important concepts in climbing is to keep your weight on your fieet as much as possible. There's a myth that climbers can hang all day on their arms. In reality, good climbers have practices specific ways of keeping their weight over their feet when possible.`

##### The Django Shell
Now that we’ve entered some data, we can examine it programatically through an interactive terminal session. This interactive environment is called the Django *shell*, and it’s a great environment for testing and troubleshooting your project. Here’s an example:
```Django title:example.sh
python manage.py shell
>>> from learning_logs.models import Topic
>>> Topic.objects.all()
<QuerySet [<Topic: Chess>, <Topic: Rock Climbing>]>
```

The command `python manage.py shell`, run in an active virtual environment, launches a Python interpreter that you can use to explore the data store in your project’s database.

Here, we import the model `Topic` from the `learning_logs.models` module. We then use the method `Topic.objects.all()` to get all instances of the model `Topic`; the list that’s returned is called a *queryset*.

We can loop over a queryset just as we’d loop over a list. Here’s how you can see the ID that’s been assigned to each topic object:
```Django title:example.py
>>> topics = Topic.objects.all()
>>> for topic in topics:
...    print(topic.id, topic)
...
1 Chess
2 Rock Climbing
```

If you know the ID of a particular object, you can use the method `Topic.objects.get()` to retrieve that object and examine any attribute the object has. Let’s look at the `text` and `date_added` values for `Chess`:
```Django title:example.sh
>>> t = Topic.objects.get(id=1)
>>> t.text
'Chess'
>>> t.date_added
>>> datetime.datetime(2022, 5, 20, 3, 33, 36, 928759, tzinfo=datetime.timezone.utc)
```

We can also look at the entries related to a certain topic. Earlier, we defined the `topic` attribute for each Entry model. This was a `ForeignKey`, a connection between each entry and a topic. Django can use this connection to get every entry related to a certain topic:
```Django title:example.sh
>>> t.entry_set.all()
>>> <QuerySet [<Entry: The opening is the first part of the game, roughtly...>, <Entry: In the opening phase of the game, it's important t...>]>
```

To get data through a foreign key relationship, you use the lowercase name of the related model followed by an underscore and the word set. For example, say you have the models `Pizza` and `Topping`, and `Topping` is related to `Pizza` through a foreign key. If your object is called `my_pizza`, representing a single pizza, you can get all of the pizza’s toppings using the code `my_pizza.topping_set.all()`.