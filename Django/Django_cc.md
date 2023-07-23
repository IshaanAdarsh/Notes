# Django:
- Django is a high-level Python web framework which is based on MVT architecture.

## MVT (Model View Template):
- The MVT is an design pattern that separates an application into three main logical componentsL
  - **Model:**
    - The Model responsible to handle database. It is a data access layer which handles the data.
    - Written in Python (Need knowledge about Databases)
  - **View:**
    - The user can send request by interacting with template, the view handles these requests and sends to Model then get appropriate response from the Model, sends response to template. It works as a mediator between Template and Model.
    - It may also have required logics (Python)
  - **Template:**
    - It represents how data should be presented to the application user. User can read or write the data from template. Basically it is responsible for showing end user content, we can say it is user interface.
    - It may consists of HTML, CSS, JS mixed with Django Template Language.

<img width="1338" alt="MVT" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/2795db0a-6c70-48b7-bdf5-e1023228f439">

## Django Project Directory Structure:
```
project_name/          # Project root directory / Outer Project Folder
|-- project_name/      # The main Django application directory / Inner Project Folder
|   |-- __init__.py
|   |-- asgi.py        # ASGI configuration (for Channels and asynchronous support)
|   |-- settings.py    # Django settings file
|   |-- urls.py        # URL configuration for the project
|   |-- wsgi.py        # WSGI configuration for deployment
|-- manage.py          # Django's command-line utility for administrative tasks
```
### `myproject/`: 
This is the root directory of your Django project. You can give it any name you prefer.

### `manage.py`: 
A command-line utility that allows you to interact with various Django commands, such as running the development server, creating database tables, etc. Its sets `DJANGO_SETTINGS_MODULE` environment variable so it points to `settings.py`.If you are working on a single Django Project it is preferred to use `manage.py` rather than `django-admin`.

### `myproject/`: 
This is the main Python package directory that contains all the settings and configurations for your project.

### `__init__.py`: 
An empty file that marks the `myproject/` directory as a Python package.

### `settings.py`: 
The settings file where you define all the configurations for your Django project, such as database settings, installed apps, middleware, etc. [Detailed Information](https://github.com/IshaanAdarsh/TIL/blob/main/Django/Extra%20files/settings_py.md)

### `urls.py`: 
The URL configuration file where you define the URL patterns and map them to view functions.

### `wsgi.py`: 
The WSGI (Web Server Gateway Interface) entry-point file used for running Django applications with traditional web servers. Work in this file when you need to interact with the web server

<img width="1385" alt="Wsgi" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/fb75ccf4-5d01-4685-81da-ff7e1361d788">

- Django uses the `DJANGO_SETTINGS_MODULE` environment variable to locate the settings module for your application. It should contain the dotted path to the settings module. If not set, the default `wsgi.py` sets it to `mysite.settings`, where `mysite` is the project name. This allows `runserver` to discover the default settings file automatically. You can use different values for development and production based on your organization of settings.

### `asgi.py`: 
The ASGI (Asynchronous Server Gateway Interface) entry-point file used for running Django applications with asynchronous servers. The successor of `wsgi.py` as it provides a standard for both synchronous and asynchronous apps

<img width="711" alt="asgi" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/6d34848a-c1ce-4d60-9f09-975293487f46">

When we run the command `python3 manage.py runserver`, some new files are created.
```
project_name/          
|-- project_name/
|   |-- __pycache__/
        (Python cache files)
|   |-- __init__.py
|   |-- asgi.py        
|   |-- settings.py    
|   |-- urls.py        
|   |-- wsgi.py        
|-- db.sqlite3
|-- manage.py
```
The new files are:
- `__pycache__/`: A directory that contains Python cache files for improved import performance.
- `db.sqlite3`: The SQLite database file where the data for your application is stored.

## Django Server Working:
Django provides built-in server which we can use to run our project. 
- `runserver` : This command is used to run built-in server of Django.

### Steps:-
- Go to Project Folder
- Then run command `python manage.py runserver`
  - Server Started. Visit `http://127.0.0.1:8000` or `http://localhost:8000`
- You can specify Port number in the end to run the project in a specific port: `python manage.py runserver 5555`
  - Visit http://127.0.0.1:5555 or http://localhost:5555

## Django Application:
### Creating a Django Application:
- A Django project contains one or more applications which means we create applications inside ProjectFolder.
Syntax:- `python manage.py startapp appname`
**Steps:**
- Go to Project Folder
- Run the syntax, if you want to create multiple applications run the syntax multiple times with different appnames.
```bash
python manage.py startapp course
```

### Installing a Django Application:
- We install application in our project using `settings.py` file. This is compulsory otherwise Application won't be recognized by Django.
**Steps:**
- Open `settings.py` file
- Add the names of the applications to the INSTALLED_APPS field and save `settings.py`
```python
# Install the applications course, fees, and result
INSTALLED APPS = [
'django.contrib.admin',
'course',
'fees',
'result',
]
```

### Application Directory Structure:
```
myapp/              # Your application's main directory
    __init__.py     # An empty file that makes this directory a Python package

    admin.py        # Configuration for the Django admin interface
    apps.py         # Application configuration
    models.py       # Database models
    tests.py        # Test cases for the application
    views.py        # Views that handle HTTP requests and render templates

    migrations/     # Directory for database migrations
        __init__.py # An empty file that makes this directory a Python package
```
- `__init__.py`: This file is required to treat the `myapp` directory as a Python package.

- `admin.py`: This file is used to register sql tables so we could perform CRUD operations from Admin Application. Admin Application is provided by Django to perform CRUD operation.

- `apps.py`: This is the configuration file for your application. It allows you to customize certain aspects of your app, such as the app's name and label.

- `models.py`: This file is used to create our own model class later these classes will be converted into a database table by Django for our application.

- `tests.py`: This file is for writing test cases to test the functionality of your application.

- `views.py`: This is where you define the views (functions or classes) that handle HTTP requests and return HTTP responses. Views are responsible for processing data and rendering templates. We write all the buisness related logic in this file/

- `migrations/`: This directory is automatically created by Django and is used to store database migration files. Migrations help you manage changes to your database schema over time. It also contains all files that are created after running `makemigration` command (keeps database-related files).

# View:
## Function Based View:
- A function-based view in Django is a Python function that handles web requests and generates web responses, such as HTML pages, redirects, or error messages.
- We use `views.py` file of the application to write functions which may contain the business logic of the application, later it is required to define url name for this function in the `urls.py` file of the project.
  - It takes an `HttpRequest` object as a parameter and returns an `HttpResponse` object to provide the response content.
```python
def function_name (request):                          # request -> httpRequest Object
  return HttpResponse('html/variable/text')           # HttpResponse -> Class
                                                      # html/variable/text -> httpResponse Object
```

### Steps:  
#### 1) Edit the Views.py:
- Where `HttpResponse` is class which is in `django.http` module so we have to import it before using `HttpResponse`.
```python
from django.http import HttpResponse

# Inside views.py different ways to use a funtion
def learn_django(request):
  return HttpResponse('Hello Django')                  # Simple Return Statement

def learn_python(request):
  return HttoResponse('<hI>Hello Puthon</hI>')         # HTML Return Statement

def learn_var(request):
  a ="<h1>Hello Variable</hi>'                         # HTML using variable
  return HttpResponse(a)

def learn_math(request):
  a = 10 + 10                                          # Maths using variable
  return HttpResponse(a)

def index(request):
  return HttpResponse('Home Page')                   # To remove the 404 error, need to specify the homepage
```

#### 2) Edit the Urls.py:
- Add the urls for the view funtion.
```python
form course import views               # Need to import the views form the application course
- urlpatterns = [
  path('admin/', admin site.urls),
  path(learndj/', views.learn_django),
  path('',views.index)                 # '' i> points to the no url so the default http://127.0.0.1:8000
]
```
- Visit the URL : http://127.0.0.1:8000          -> Homepage
- Visit the URL : http://127.0.0.1:8000/learndj/ -> Hello Django


