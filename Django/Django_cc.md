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

## URL Dispatcher:
- To design URLs for app, you create a Python module informally named urls.py. This module is pure Python code and is a mapping between URL path expressions to view functions.

![URL-Dispatcher](https://github.com/IshaanAdarsh/TIL/assets/100434702/af7bcaa9-5450-4375-931e-fea234a800c0)

### path ( )
`path(route, view, kwargs=None, name=None)` : It returns an element for inclusion in urlpatterns.
- The route argument must be a string or gettext_lazy() containing a URL pattern with angle brackets (<>) to capture parts of the URL as keyword arguments for the view.
  - Angle brackets can include converter specifications like <int:id> to limit characters matched and change the variable type passed to the view (e.g., converting to an integer).
- The view argument is a view function or the result of as view for class-based views.
It can also be an django.urls.include.
- The kwargs argument allows you to pass additional arguments to the view function or method. It should be a dictionary.
- name is used to perform URL reversing.

```python
# urls.pr Sample Syntax
urlpatterns = [
  path(route, view, kwargs=None, name=None)
]

# urls.py Example
urlpatterns = [
  path(learndj/', views.learn_Django, {'check': 'OK'), name= 'learn django'),
]
```

### Steps to use View Funtion and URL Dispatcher at Project level:  
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
form course import views                         # Need to import the views form the application course

# Update the urls to point to the new changes
urlpatterns = [
  path('admin/', admin site.urls),
  path(learndj/', views.learn_django),
  path('',views.index),                          # '' -> points to the no url so the default http://127.0.0.1:8000
  path(altlearndj/, views.learn_Django),         # We can define multiple url for one view function.
]
```
- Visit the URL : http://127.0.0.1:8000          -> Homepage
- Visit the URL : http://127.0.0.1:8000/learndj/ -> Hello Django

### Multiple Application inside Project and their Function Based Views:
- Add funtions to the `views.py` of the individual applications and then add thier details in the `urls.py` of the main folder.

```python
# Incorrect urls.py
# As they have the same name (views), we have to sepcify which views.py we are talking about. Is it the course.view or fees.views
from course import views
from fees import views
  urlpatterns = [
    path(learndj/', views.learn_django),
    path(feesdj/', views.fees _django),
]

# Correct urls.py
# Method 1: Aliasing
from course import views as cv
from fees import views as fv
  urlpatterns = [
    path(learndj/', cv.learn_django),
    path(feesdj/', fv.fees _django),
]

# Method 2: Individual funtions (More reductive, not preferred)
urls.py
from course.views import learn_django
from fees.views import fees _django
  urlpatterns = [
    path (learndj/', learn_django),
    path (feesdj/', fees_django),
]
```
- But our each application should be independent or less depend on project so we could use our applications in different projects easily without worrying about `urls.py` available in Project Folder. We need to use url pattern inside Application to Reduce the dependency of Application, Enhance Application performance and Reusability of application becomes easy.

### View Funtion and URL Pattern inside Application:  
#### include():
- The `include()` function in Python includes another URLconf module using its import path. It can take optional arguments for specifying namespaces and accepts an iterable or a 2-tuple containing URL patterns and application namespaces. This allows for flexible and modular URL configuration.
- `path(route, view, kwargs=None, name=None)`
- The view argument is a view function or the result of as view for class-based views. It can also be an django.urls.include.

```python
# Syntax
Syntax:-
include(module, namespace=None)
include(pattern list)
include((pattern_ list, app_ namespace), namespace=None)

# Example:
# Method 1: straight linking
from django.urls import include, path
  urlpatterns = [
    path('cor/', include('course.urls')),
]

# Method 2: Using Lists
urlpatterns = [
  path('cor/', include([
    path('learndj/', views.learn _django),
    path('learnpy/', views.learn_python)
  ])),
]

# Same as above code:
otherpatterns = [
  path('learndj/', views.learn django),
  path('learnpy/', views.learn python),
]
urlpatterns = [
path('cor/', include(otherpatterns),
]
```

### Steps: 
#### Write URL Pattern inside Application
- Create an `urls.py` file inside each application (in case multiple application).
- Write all url pattern related to application, in `urls.py` file available inside application.
- Include Application's `urls.py` file inside Project's `urls.py` file.

```python
# views.py in Application Folder
from django.http import HttpResponse
def learn_django(request):
  return HllpResponse('Hello Django')
def learn_python(request):
  return HttpResponse(*<hI>Hello Python</hI>')

# urls.py in Application Folder
from course import views
  urlpatterns = [
    path('learndj/', views.learn django),
    path(learnpy/', views.learn_python),
]

# urls.py in Project Folder
from django.urls import path, include
urlpatterns = [
  path(cor/, include('course.urls')),          # course -> Package Name, urls -> Module Name
]
```
Links to viist the applications:
- http://127.0.0.1:8000/cor/learndj 
- http://127.0.0.1:8000/cor/learnpy

# Template:
- A template is a text file. It can generate any text-based format (HTML, XML, CSS, etc). It contains variables, which get replaced with values when the template is evaluated, and tags, which control the logic of the template. Template is used by view function to represent the data to user.

### Creating Templates:
- We create `templates` folder inside Project Folder,this folder will contain all HTML files.
- Add templates in `settings.py`
  - Create a variable `TEMPLATES_DIR` and add it to the `TEMPLATES` List

```python
# settings.py
TEMPLATES_DIR = os.path.join(BASE_DIR,'templates')

TEMPLATES = [
  {
    'DIRS': [TEMPLATES _ DIR],
    # Directories where the engine should look for template source files, in search order.
  }
]
```

### Writing Template Files:
- When we create Template file for application we separate business logic and presentation from the application views.py file.
- We write business logic in views py file and presentation code in template file.

### Rendering Templates Files:
- Still `views.py` will be responsible to process the template files for this we will use `render()` function in `views.py` file.
### render ()
- `render() Function`: It combines a given template with a given context dictionary and returns an HttpResponse object with that rendered text.

`render(request, template_name, context=dict _ name, content_type=MIME_type, status=None, using=None)`

- **request**: The request object used to generate this response. */
- **template_name**: The full name of a template to use or sequence of template names. If a sequence is given, the first template that exists will be used. */
- **context**: A dictionary of values to add to the template context. By default, this is an empty dictionary. If a value in the dictionary is callable, the view will call it just before rendering the template.
- **content_type**: The MIME type to use for the resulting document. Defaults to 'text/html'.
- **status**: The status code for the response. Defaults to 200.
- **using**: The NAME of a template engine to use for loading the template.

> */ -> Manatory Fields to include for the reder function to execute

```python
# views.py
from django.shortcuts import render
def function name(request):
  # Dynamic Data can be written, if else, any python code logic
    return render(request, template _ name, context=dict name,
    content_type=MIME_type, status=None, using=None)

# Example:
def learn django(request):
  return render(request, 'courseone.html')

# Example:
def learn django(request):
  render(request,'courseone.html',context=cname,content_type='application/xhtml+xml')
```

### Creating and Rendering Templates File For each Application Separately:
- We can create separate folder inside templates folder for applications then each application will contain only those HTML file which are related to them. This will enhance readability and separate HTML files according to applications.

![Template_naming](https://github.com/IshaanAdarsh/TIL/assets/100434702/865f261c-0f8d-4bda-9433-757517c996f9)

- Follow the same steps for the writing and creating of template files (just make seperate files for more clarity)
- Just in the Rendering Process of the templates edit the template name to reflect the template path

```python
# views.py
def learn django(request):
  return render(request,'course/courseone.html')          # Reflects the chnae form courseone.html to new location
```

## Dynamic Template Files using DTL:
- For more detailed information about [DLT](https://github.com/IshaanAdarsh/TIL/blob/main/Django/Detailed%20Information/DLT.md)
- Use variables in the HTML files using Django Template Language
```python
# views.py
from django.shortcuts import render
def function name(request):
  # Dynamic Data, if else, any python code logic
    return render(request, template _name, context=dict_name, content_type=MIME_type, status=None, using=None)

# views.py
from django.shortcuts import render
def learn_django(request):
  coursename = {'cname': 'Django'}
  return render(request, 'course/courseone.html', context coursename)
  # OR
  return render(request, 'course/courseone. html', coursename)
  # OR
  return render(request,'course/courseone.html',{'cname': 'Django'})

# Example:
# views.py
from django.shortcuts import render
def learn django(request):
    cname = 'Django'
    duration = '4 Months
    seats = 10
    django_details = ('nm' :cname, 'du': duration, 'st' :seats}
    return render(request, 'course/courseone.html', django_details)
```
- Write the HTML using the variables
```html
// courseone.html
<html>
  <body>
    <h2> Course Name: {{nm}} Duration: {{du}} and Total Seats: {{st}}</h2>
  </body>
</html>
```

