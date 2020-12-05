# DjangoProject
## Day-3 

## Templates and Inheritance
A template is a text file. It can generate any text-based format (HTML, XML, CSV, etc.).
A template contains variables, which get replaced with values when the template is evaluated, and tags, which control the logic of the template.

Our templates needs to be stored in app_folder-> templates-> app_name-> template_name.html. To display that template using function we can use `render() method`. 
  ```
  def home(request):
    return render(request, 'accounts/dashboard.html')
  ```
Here, accounts is the name of the directory in templates directory where our templates are present. When lot of templates needs to used, we could get a lot of redundant code. So, to solve this issue, we can create a base template (main.html). In the base template, we can create our header and footer, so we don't want to repeat the code. Block tages are used for making the page more dynamic. 
  ```
    {% block content %}
    
    
    {% endblock %}
  ```
Now, the child template can reside in this section. In order to use the base template, the child template need to extend the base template.
  ```
  {% extends 'path_of_base_template' %}
  ```
Now, we need to specify the section and add the content in the section. Alseo, we can have our header, footer in the  differents template. To have header, footer in a different
templates, create new templates, add the code and include it in the base template.
  ```
  {% include 'path_of_template' %}
  ```
We can add our css and javascript code in the base template and only html code in the other template(header, footer, etc...). 
