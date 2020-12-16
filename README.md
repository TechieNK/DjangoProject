# DjangoProject
## Day-4 
## Static Files & Images
Websites generally need to serve additional files such as images, JavaScript, or CSS. In Django, we refer to these files as “static files”. When you have a lot a code, it's a lot better to have one centralized area to store our CSS, JavaScript, or images. First, create a directory called `static` in your project directory and inside `static` directory create respective folders for CSS, JavaScript, and images. Django will look for static files there, similarly to how Django finds templates.

Open the settings.py file inside the inner djangotemplates folder. At the very bottom of the file you should see these lines:
```
# djangotemplates/djangotemplates/settings.py

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.10/howto/static-files/

STATIC_URL = '/static/'
 ```
This line tells Django to append static to the base url when searching for static files. In Django, you could have a static folder almost anywhere you want. You can even have more than one static folder e.g. one in each app. For now, let’s add some lines in the settings.py file so that it looks like this.
```
# djangotemplates/djangotemplates/settings.py

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/1.10/howto/static-files/

STATIC_URL = '/static/'

# Add these new lines
STATICFILES_DIRS = (
    BASE_DIR / 'static'
)

STATIC_ROOT = os.path.join(BASE_DIR, 'staticfiles')
```
The STATICFILES_DIRS tuple tells Django where to look for static files that are not tied to a particular app. In this case, we just told Django to also look for static files in a folder called static in our root folder, not just in our apps. Django also provides a mechanism for collecting static files into one place so that they can be served easily. Using the collectstatic command, Django looks for all static files in your apps and collects them wherever you told it to, i.e. the STATIC_ROOT. 

Now, we can import these static files into our template. To tell the template engine to use the files in the static folder in that template,  we need to add Django's special template tag syntax `{% load static %}`. To use the CSS files from static folder in our template, we need to link the css files and provide the path in the `href` attribute, which looks like
```
<link rel="stylesheet" type="text/css" href="{% static '/css/main.css' %}">
```
where `main.css` is the name of css file which is present in the css folder.
