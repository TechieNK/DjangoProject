# DjangoProject
## Day-10

## Django CRUD (Create, Retrieve, Update, Delete) Function Based Views
In general CRUD means performing Create, Retrieve, Update and Delete operations on a table in a database.

* **Create** – create or add new entries in a table in the database.
* **Retrieve** – read, retrieve, search, or view existing entries as a list(List View) or retrieve a particular entry in detail (Detail View)
* **Update** – update or edit existing entries in a table in the database
* **Delete** – delete, deactivate, or remove existing entries in a table in the database

We need to create a modelForm for a model.
```
from django.forms import ModelForm
from . models import *

class OrderForm(ModelForm):
	class Meta:
		model = Order
		fields = '__all__'
		
```
For need to create a view for update, delete and create operations.

**Create View**
```
def createOrder(request):

	form = OrderForm()
	if request.method=='POST':
		form = OrderForm(request.POST)
		if form.is_valid():
			form.save()
			return redirect('/')
			
	context = {'form':form}
	return render(request, 'accounts/order_form.html',context)
```
To use the **redirect()** we need to import it from `django.shortcuts`. **is_valid()** will check the validation of the form. **save()** will save the order in the database.

**Update View**
```
def updateOrder(request, pk):

	order = Order.objects.get(id=pk)
	form = OrderForm(instance=order)

	if request.method == 'POST':
		form = OrderForm(request.POST, instance=order)
		if form.is_valid():
			form.save()
			return redirect('/')

	context = {'form':form}
	return render(request, 'accounts/order_form.html', context)	
```
**Delete View**
```
def deleteOrder(request, pk):
	order = Order.objects.get(id=pk)
	if request.method == "POST":
		order.delete()
		return redirect('/')

	context = {'item':order}
	return render(request, 'accounts/delete.html', context)
```
Also, we need to create a template for creating and updating orders and for deleting orders.

## Cross Site Request Forgery protection
The CSRF middleware and template tag provides easy-to-use protection against Cross Site Request Forgeries. This type of attack occurs when a malicious website contains a link, a form button or some JavaScript that is intended to perform some action on your website, using the credentials of a logged-in user who visits the malicious site in their browser.

## How to use it
To take advantage of CSRF protection in your views, follow these steps:

1. The CSRF middleware is activated by default in the **MIDDLEWARE setting**. If you override that setting, remember that **'django.middleware.csrf.CsrfViewMiddleware'** should come before any view middleware that assume that CSRF attacks have been dealt with.

  If you disabled it, which is not recommended, you can use **csrf_protect()** on particular views you want to protect (see below).

2. In any template that uses a POST form, use the **csrf_token** tag inside the <**form**> element if the form is for an internal URL, e.g.:
  ```
  <form method="post">{% csrf_token %}
  ```
  This should not be done for POST forms that target external URLs, since that would cause the CSRF token to be leaked, leading to a vulnerability.

3. In the corresponding view functions, ensure that **RequestContext** is used to render the response so that **{% csrf_token %}** will work properly. 

**order_form.html**
```
{% extends 'accounts/main.html' %} 
{% load static %} 
{% block content %} 

<form action="" method="POST">
  {% csrf_token %}
  {{form}}

  <input type="submit" name="Submit">
</form>
{% endblock %}
```
**delete.html**
```
{% extends 'accounts/main.html' %}
{% load static %}
{% block content %}

<p>Are you sure you want to delete "{{item}}"?</p>
<form action="{% url 'delete_order' item.id  %}" method="POST">
  {% csrf_token %}
  <a href="{% url 'home' %}">Cancel</a>
  <input type="submit" name="Confirm">
</form>
{% endblock %}
```
