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
The settings file where you define all the configurations for your Django project, such as database settings, installed apps, middleware, etc.

### `urls.py`: 
The URL configuration file where you define the URL patterns and map them to view functions.

### `asgi.py`: 
The ASGI (Asynchronous Server Gateway Interface) entry-point file used for running Django applications with asynchronous servers. The successor of `wsgi.py` as it provides a standard for both synchronous and asynchronous apps

### `wsgi.py`: 
The WSGI (Web Server Gateway Interface) entry-point file used for running Django applications with traditional web servers. Work in this file when you need to interact with the web server

<img width="1385" alt="Wsgi" src="https://github.com/IshaanAdarsh/TIL/assets/100434702/fb75ccf4-5d01-4685-81da-ff7e1361d788">

- Django uses the `DJANGO_SETTINGS_MODULE` environment variable to locate the settings module for your application. It should contain the dotted path to the settings module. If not set, the default `wsgi.py` sets it to `mysite.settings`, where `mysite` is the project name. This allows `runserver` to discover the default settings file automatically. You can use different values for development and production based on your organization of settings.

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

