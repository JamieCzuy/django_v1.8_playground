# django_v1.8_playground
Playground for Django v1.8 (using Python 3.4)

Install DJango
--------------

From [install Url](https://docs.djangoproject.com/en/1.8/intro/install/):

    pip install django
    python -c "import django; print(django.get_version())"


Tutorial Part1 [link](https://docs.djangoproject.com/en/1.8/intro/tutorial01/)
===================

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
This has to be done whenever this repo is cloned to a new folder.

    python src/manage.py migrate

Run Development Server:
-----------------------

    python src/manage.py runserver

Verify it is running:
---------------------

    open http://127.0.0.1:8000/

Create the Polls app:
---------------------

    cd src
    python manage.py startapp polls
    cd ..

Edit src/polls/models.py:
-------------------------

    vim src/polls/models.py

    from django.db import models


    class Question(models.Model):
        question_text = models.CharField(max_length=200)
        pub_date = models.DateTimeField('date published')


    class Choice(models.Model):
        question = models.ForeignKey(Question)
        choice_text = models.CharField(max_length=200)
        votes = models.IntegerField(default=0)

Add the Polls app to the Project:
---------------------------------

    vim src/project01/settings.py

    Find list of installed apps (line 33) and add
      'polls',
    after 'django.contrib.staticfiles',

Create migration for Polls app:
-------------------------------

This creates a migration "script" to be used to add the
Polls model to the database.

    python src/manage.py makemigrations polls

Verify what the migration will do:
----------------------------------

    python src/manage.py sqlmigrate polls 0001

Apply the migration:
--------------------

    python src/manage.py migrate

Play in the Django shell:
-------------------------

    python src/manage.py shell

    (create a question)

Update Polls app's model:
-------------------------

    vim src/polls/models.py

    import datetime

    from django.db import models
    from django.utils import timezone

    class Question(models.Model):
        question_text = models.CharField(max_length=200)
        pub_date = models.DateTimeField('date published')
        def __str__(self):
            return self.question_text
        def was_published_recently(self):
            return self.pub_date >= timezone.now() - datetime.timedelta(days=1)

    class Choice(models.Model):
        question = models.ForeignKey(Question)
        choice_text = models.CharField(max_length=200)
        votes = models.IntegerField(default=0)
        def __str__(self):
            return self.choice_text

Tutorial Part2 [link](https://docs.djangoproject.com/en/1.8/intro/tutorial02/)
===================

Create admin user:
------------------

    python src/manage.py createsuperuser

    Username: admin
    Email Address: <use your own>
    Password: <password>
    Password (again): <password>

Play in the admin form:
-----------------------

    open http://127.0.0.1:8000/admin/

Add Poll app to admin form:
---------------------------

The tutorial goes through the changes one at a time but here is the final
version of Polls admin.py


    vim src/polls/admin.py


    from django.contrib import admin

    from .models import Question
    admin.site.register(Question)
