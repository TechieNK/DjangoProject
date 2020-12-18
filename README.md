# DjangoProject
## Day-5 
## The Django Admin
A web-based administrative backend is a standard feature of modern websites. The administrative interface, or admin for short, allows trusted site administrators to create, edit and publish content, manage site users, and perform other administrative tasks.

Django comes with a built-in admin interface. With Django’s admin you can authenticate users, display and handle forms, and validate input; all automatically. Django also provides a convenient interface to manage model data.

## Accessing the Django Admin Site
Create an admin user (superuser) to log into the admin site. To create an admin user, run the following command:
```
python manage.py createsuperuser
```
Enter your desired username and press enter:
```
Username: admin
```
Django then prompts you for your email address:
```
Email address: admin@example.com
```
The final step is to enter your password. Enter your password twice, the second time to confirm your password:
```
Password: **********
Password (again): *********
Superuser created successfully.
```
Now you have created an admin user, you’re ready to use the Django admin. Let’s start the development server and explore.

First, make sure the development server is running, then open a web browser to http://127.0.0.1:8000/admin/. Log in with the superuser account you created. At the top of the index page is the Authentication and Authorization group with two types of editable content: Groups and Users. They are provided by the authentication framework included in Django. 

## Models
A model is the single, definitive source of information about your data. It contains the essential fields and behaviors of the data you’re storing. It is a class that represents table or collection in our DB, and where every attribute of the class is a field of the table or collection.  In short, Django Models is the SQL of Database one uses with Django. SQL (Structured Query Language) is complex and involves a lot of different queries for creating, deleting, updating or any other stuff related to database. Django models simplify the tasks and organize tables into models. Models are defined in the app/models.py

The basics:

* Each model is a Python class that subclasses **django.db.models.Model**.
* Each attribute of the model represents a database field.
* With all of this, Django gives you an automatically-generated database-access API

## Quick example 

