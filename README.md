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
A many to many relationship implies that many records can have many other records associated amongst one another. For example, `Store` model records can have many `Amenity` records, just as `Amenity` records can belong to many `Store` records. To define a many to many relationship in Django models you use the `ManyToManyField` data type. Listing 7-23 illustrates a sample of a many to many Django relationship.
```
from django.db import models

class Amenity(models.Model):
    name = models.CharField(max_length=30)
    description = models.CharField(max_length=100)

class Store(models.Model):
    name = models.CharField(max_length=30)    
    address = models.CharField(max_length=30)
    city = models.CharField(max_length=30)
    state = models.CharField(max_length=2)
    email = models.EmailField()
    amenities = models.ManyToManyField(Amenity,blank=True)
```
The first Django model in the above example is `Amenity` and has the `name` and `description` fields. Next, in the above example is the `Store` Django model which has the `amenities` field, that itself has the `models.ManyToManyField(Amenity,blank=True)` definition. The `models.ManyToManyField()` definition creates the many to many relationship via a junction table, where the first argument `Amenity` indicates the relationship model and the optional `blank=True` argument allows a `Store` record to be created without the need of an `amenities` value.

In this case, the junction table created by Django is used to hold the relationships between the `Amenity` and `Store` records through their respective keys. Although you don't need to manipulate the junction table directly, for reference purposes, Django uses the syntax `<model_name>_<model_field_with_ManyToManyField>` to name it (e.g. For `Store` model records stored in the `stores_store` table and `Amenity` model records stored in the `stores_amenity` table, the junction table is `stores_store_amenities`)
