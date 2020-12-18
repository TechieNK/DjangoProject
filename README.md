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
A many to many relationship implies that many records can have many other records associated amongst one another. For example, `Store` model records can have many `Amenity` records, just as `Amenity` records can belong to many `Store` records. To define a many to many relationship in Django models you use the `ManyToManyField` data type.
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

## One to one relationships in Django models
A one to one relationship implies that one record is associated with another record. If you're familiar with object-orientated programming, a one to one relationship in RDBMS is similar to object-oriented inheritance that uses the is a rule (e.g. a Car object is a Vehicle object).

For example, generic `Item` model records can have a one to one relationship to `Drink` model records, where the latter records hold information specific to drinks (e.g. caffeine content) and the former records hold generic information about items (e.g. price). To define a one to one relationship in Django models you use the `OneToOneField` data type.
```
from django.db import models

class Menu(models.Model):
    name = models.CharField(max_length=30)

class Item(models.Model):
    menu = models.ForeignKey(Menu)
    name = models.CharField(max_length=30)
    description = models.CharField(max_length=100)
    calories = models.IntegerField()
    price = models.FloatField()

class Drink(models.Model):
    item = models.OneToOneField(Item,on_delete=models.CASCADE,primary_key=True)
    caffeine = models.IntegerField()
```
The first Django model in the above example is `Item` which is similar to the one presented in one to many relationship example, except the version in the above example has the additional `calories` and `price` fields. Next, in the above example is the `Drink` model which has the `item` field, that itself has the `models.OneToOneField(Amenity,on_delete=models.CASCADE,primary_key=True)` definition.

The `models.OneToOneField()` definition creates the one to one relationship, where the first argument `Item` indicates the relationship model. The second argument `on_delete=models.CASCADE` tells Django that in case the relationship record is deleted (i.e. the `Item`) its other record (i.e. the `Drink`) also be deleted, this last argument prevents orphaned data. Finally, the `primary_key=True` tells Django to use the relationship id (i.e. `Drink.id`) as the primary key instead of using a separate and default column `id`, a technique that makes it easier to track relationships.
