# DjangoProject
## Day-11

## Inline formsets
**class models.BaseInlineFormSet**

Inline formsets is a small abstraction layer on top of model formsets. These simplify the case of working with related objects via a foreign key. Suppose you have these two models:
```
from django.db import models

class Author(models.Model):
    name = models.CharField(max_length=100)

class Book(models.Model):
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    title = models.CharField(max_length=100)
```
If you want to create a formset that allows you to edit books belonging to a particular author, you could do this:
```
>>> from django.forms import inlineformset_factory
>>> BookFormSet = inlineformset_factory(Author, Book, fields=('title',))
>>> author = Author.objects.get(name='Mike Royko')
>>> formset = BookFormSet(instance=author)
```
**BookFormSet**’s prefix is **'book_set'** (**<model name>_set** ). If **Book**’s **ForeignKey** to **Author** has a **related_name**, that’s used instead.

**Note**: **inlineformset_factory()** uses **modelformset_factory()** and marks **can_delete=True**.

