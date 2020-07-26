# tutorial-django-1

## install up django (ubuntu 20.04)
```
create & start a virtualenv (optional)

pip3 install django

django-admin startproject <project_name>

python3 project_name/manage.py runserver
```
<!-- python manage.py startapp app_name -->
At this point you should be able to visit http://127.0.0.1:8000/ and see the default django page, with the text:

>You are seeing this page because DEBUG=True is in your settings file and you have not configured any URLs
---

## hello world

```
Create a new app:
---

cd to manage.py

python3 manage.py startapp <app_name>
```

```
Append new app to the main project:
---

code project_name/settings.py

<-- Start code section -->
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    '<app_name>'
]
<-- End code section -->
```

```
Create hello world route:
---

code app_name/views.py

<-- Start code section -->
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def index(request):
    return HttpResponse('hello, World!')
<-- End code section -->
```

```
Link the functions in views to url routes
---

touch app_name/urls.py
code app/name/urls.py

<-- Start code section -->
from django.urls import path

from . import views

urlpatterns = [
    path("", views.index, name="index")
]
<-- End code section -->
```

```
Link the urls in the new app to the main project
---

code project_name/urls.py

<-- Start code section -->
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('<url-prefix>/', include('<app_name>.urls'))
]
<-- End code section -->
```

## heroku
Be in root directory
```
create heroku app:
---

heroku login

heroku create <app>
```

```
gunicorn setup:
---

pip3 install gunicorn
```

```
running gunicorn locally:
---

gunicorn --chdir <project_name>/ <project_name>.wsgi
# gunicorn: command to start the gunocron server
# --chdir: command to change directory
# <project_name>/: path for the change directory
# <project_name>.: further path for where the run file is found
# wsgi: the name of the run file
```

```
Create heroku Procfile
---

touch Procfile
code Procfile

<-- Start code section -->
web: gunicorn --chdir <project_name>/ <project_name>.wsgi
<-- End code section -->
```

```
Updating allowed hosts (for local testing)
---
code <project_name>/<project_name>/settings.py

<-- Start code section -->
ALLOWED_HOSTS = ['0.0.0.0']
<-- End code section -->

Testing heroku locally
---
heroku local
```

```
import django_heroku

# Activate Django-Heroku.
django_heroku.settings(locals())
```

```
Requirments
---
pip3 freeze > requirements.txt
```