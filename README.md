# DjangoProject
## Day-6 

## Relationships in Django models
Django models operate by default on relational database systems (RDBMS) and thus they also support relationships amongst one another. In the simplest terms, database relationships are used to associate records on the basis of a key or id, resulting in improved data maintenance, query performance and less duplicate data, among other things.

Django models support the same three relationships supported by relational database systems: One to many, many to many and one to one.

## One to many relationships in Django models
A one to many relationship implies that one model record can have many other model records associated with itself. For example, a `Menu` model record can have many `Item` model records associated with it and yet an `Item` belongs to a single `Menu` record. To define a one to many relationship in Django models you use the `ForeignKey` data type on the model that has the many records (e.g. on the `Item` model).

```
from django.db import models

class Menu(models.Model):
    name = models.CharField(max_length=30)

class Item(models.Model):
    menu = models.ForeignKey(Menu)
    name = models.CharField(max_length=30)
    description = models.CharField(max_length=100)
```
The first Django model in the above example is `Menu` and has the `name` field (e.g. `Menu` instances can be `Breakfast`, `Lunch`, `Drinks`,etc). Next, in the above example is the `Item` Django model which has a `menu` field, that itself has the `models.ForeignKey(Menu)` definition. The `models.ForeignKey()` definition creates the one to many relationship, where the first argument Menu indicates the relationship model.

## Many to many relationships in Django models
