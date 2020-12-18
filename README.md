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
* With all of this, Django gives you an automatically-generated database-access API:

## Writing models in Python has several advantages:

* **Simplicity**: Writing Python is not only easier than writing SQL, but it’s less error-prone and more efficient as your brain doesn’t have to keep switching from one language to another.
* **Consistency**: As I mentioned earlier, SQL is inconsistent across different databases. You want to describe your data once, not create separate sets of SQL statements for each database to which the application will be deployed.
* **Avoids Introspection**: Any application has to know something about the underlying database structure. There are only two ways to do that: have an explicit description of the data in the application code, or introspect the database at runtime. As introspection has a high overhead and is not perfect, Django’s creators chose the first option.
* **Version Control**: Storing models in your codebase makes it easier to keep track of design changes.
* **Advanced Metadata**: Having models described in code rather than SQL allows for special data-types (e.g., email addresses), and provides the ability to store much more metadata than SQL.

A drawback is the database can get out of sync with your models, but Django takes care of this problem with migrations.

## Quick example 
This example model defines a **Person**, which has a **first_name** and **last_name**:
```
from django.db import models

class Person(models.Model):
    first_name = models.CharField(max_length=30)
    last_name = models.CharField(max_length=30)
```
**first_name** and **last_name** are fields of the model. Each field is specified as a class attribute, and each attribute maps to a database column.

The above **Person** model would create a database table like this:
```
CREATE TABLE myapp_person (
    "id" serial NOT NULL PRIMARY KEY,
    "first_name" varchar(30) NOT NULL,
    "last_name" varchar(30) NOT NULL
);
```
## Fields
A model can have an arbitrary number of fields, of any type — each one represents a column of data that we want to store in one of our database tables. Each database record (row) will consist of one of each field value. Let's look at the example seen below:
```
first_name = models.CharField(max_length=20, help_text='Enter field documentation')
```
Our above example has a single field called **first_name**, of type models.CharField — which means that this field will contain strings of alphanumeric characters. The field types are assigned using specific classes, which determine the type of record that is used to store the data in the database, along with validation criteria to be used when values are received from an HTML form (i.e. what constitutes a valid value). The field types can also take arguments that further specify how the field is stored or can be used. In this case we are giving our field two arguments:

* `max_length=20` — States that the maximum length of a value in this field is 20 characters.
* `help_text='Enter field documentation'` — provides a text label to display to help users know what value to provide when this value is to be entered by a user via an HTML form.

The field name is used to refer to it in queries and templates. Fields also have a label specified as an argument (`verbose_name`), the default value of which is `None`, meaning replacing any underscores in the field name with a space (for example first_name would have a default label of first name). Note that when the label is used as a form label through Django frame, the first letter of the label is capitalised (for example first_name would be First name).

The order that fields are declared will affect their default order if a model is rendered in a form (e.g. in the Admin site), though this may be overridden.

