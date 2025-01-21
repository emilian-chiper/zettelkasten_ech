### Meta
2025-01-21 11:20
**Tags:** [[py_projects]] [[py_web_app]] [[py_wap_django]]
**Status:** #completed 

#### Setting Up a Project
When starting work on something as significant as a web app (lmao), you first need to describe the project’s goals in a specification, or *spec*. Once you have a clear set of goals, you can start to identify manageable tasks to achieve those goals.

##### Writing a Spec
A full spec details the project goals, describes the project’s functionality, and discusses its appearance and user interface. Here’s the spec we’ll use:
`We'll write a web app called Learning Log that allows users to log the topics they're interested in and make journal entries as they learn about each topic. The Learning Log home page will describe the site and invite users to either register or log in. Once logged in, a user can create new topics, add new entries, and read and edit existing entries.`

##### Creating a Virtual Environment
To work with Django, we’ll first set up a virtual environment. A *virtual environment* is a place on your system where you can install packages and isolate them from all other Python packages. Separating one project’s libraries from other projects is beneficial and will be necessary during deployment.

To create a virtual environment, open terminal and switch to the working directory, entering the following code:
```BASH title:example.sh
python -m venv ll_env
# or
python3 -m venv ll_env
```

Here we’re running the `venv` virtual environment module and using it to create an environment named *ll_env*.

##### Activating the Virtual Environment
Now we must activate the virtual environment, using the following command:
```BASH title:example.sh
source ll_env/bin/activate
```

This command runs the script *activate* inside *ll_env/bin*. When the environment is active, you’ll see its name in parentheses. This indicates that you can install new packages to the environment and use packages that have already been installed. Packages you install in *ll_env* will not be available when the environment is inactive.

To stop using a virtual environment, enter `deactivate`. The environment will also become inactive when you close the terminal it’s running in.

##### Installing Django
Withe the virtual environment activated, enter the following to update pip and install Django:
```BASH title:example.sh
pip install --upgrade pip
pip install django
```

It’s a good idea to upgrade pip whenever you make a new virtual environment. The command to install Django is the same on all systems. There’s no need to use longer commands, such as `python -m pip install package_name`, or to include the `--user` flag.

##### Creating a Project in Django
Without leaving the active virtual environment (remember to look for *ll_env* in terminal prompt), enter the following commands to create a new project:
```BASH title:example.sh
django-admin startproject ll_project .
ls
ll_env ll_project manage.py
ls ll_project
__init__.py asgi.py settings.py urls.py wsgi.py
```

The `startproject` command tells Django to set up a new project called *ll_project*. The dot at the end of the command creates a new project with a directory structure that will make it easy to deploy the app to a server when we’re finished developing it.

**Note:** Don’t forget this dot, or you might run into some configuration issues when you deploy the app. If you forget the dot, delete the files and folders that were created (except `ll_env`) and run the command again.

##### Creating the Database
Django stores most of the information for a project in a database, so next we must create a database that Django can work with. Enter the following command (still in active environment):
```BASH title:example.sh
python3 manage.py migrate
ls
db.sqlite3 ll_env ll_project manage.py
```

Anytime we modify a database, we say we’re *migrating* the database. Issuing the `migrate` command for the first time tells Django to make sure the database matches the current state of the project. The first time we run this command in a new project using SQLite, Django will create a new database for us. Here, Django reports that it will prepare the database to store information it needs to handle administrative and authentication tasks.

Running the `ls` command shows that Django created another file called *db.sqlite3*. *SQLite* is a database that runs off a single file; it’s ideal for writing simple apps because you won’t have to pay much attention to managing the database.

##### Viewing the Project
To ensure that Django has set up the project properly, enter the `runserver` command as follows:
```BASH title:example.sh
python manage.py runserver
```

Django should start a server called the *development server*, so you can view the project on your system to see how well it works. When you request a page by entering a URL in a browser, the Django server responds to that request by building the appropriate page and sending it to the browser.

Django first checks to make sure the project is set up properly; it then reports the version of Django in use and the name of the settings file in use. Finally, it reports teh URL where the project is being served. The URL `http://127.0.0:8000` indicates that the project is listening for requests on port 8000 on your computer, which is called a *localhost*. The term refers to a server that only processes requests on your system; it doesn’t allow anyone elese to see the pages you’re developing.

Clicking on the localhost URL in terminal should open the project’s web page in your default browser. You can use `Ctrl-C` in terminal where `runserver` was issued to stop the server.

**Note:** If you receive the error message “That port is already in use”, tell Django to use a different port by entering `python manage.py 8001` and then cycling through higher numbers until you find an open port. 
