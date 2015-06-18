# django_v1.8_playground
Playground for Django v1.8 (using Python 3.4)

Install DJango
--------------

From [install Url](https://docs.djangoproject.com/en/1.8/intro/install/):

    pip install django
    python -c "import django; print(django.get_version())"

Create A Project:
-----------------

    django-admin startproject project01
    mv project01 src

Set Time Zone:
--------------

    vim src/project01/settings.py
    Change time zone (line 90 - to 'EST')

Create DB Tables:
-----------------

    python src/manage.py migrate

Run Development Server:
-----------------------

    python src/manage.py runserver

Verify it is running:
---------------------

    open http://127.0.0.1:8000/
