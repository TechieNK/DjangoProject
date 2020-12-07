# DjangoProject
## Day-3 Hello

## Templates
A template is a text file. It can generate any text-based format (HTML, XML, CSV, etc.).
A template contains variables, which get replaced with values when the template is evaluated, and tags, which control the logic of the template.

Our templates needs to be stored in app_folder-> templates-> app_name-> template_name.html. To display that template using function we can use `render()` method. 
  ```
  def home(request):
    return render(request, 'accounts/dashboard.html')
  ```
Here, `accounts` is the name of the directory in templates directory where templates are present and `dashboard.html` is our template . 

### Tags
Tags look like this: `{% tag %}`. Tags are more complex than variables: Some create text in the output, some control flow by performing loops or logic, and some load external information into the template to be used by later variables. Some tags require beginning and ending tags (i.e. `{% tag %} ... tag contents ... {% endtag %}`).
Django ships with about two dozen built-in template tags.

When lot of templates needs to used, we could get a lot of redundant code. So, to solve this issue, we use the concept of template inheritance. 

## Template inheritance
The most powerful – and thus the most complex – part of Django’s template engine is template inheritance. Template inheritance allows you to build a base template that contains all the common elements of your site and defines blocks that child templates can override. For that a section need to be added in the base template.
  ```
    {% block content %}
    
    
    {% endblock %}
  ```
Now, the child template can reside in this section. In order to use the base template, the child template need to extend the base template.
  ```
  {% extends 'path_of_base_template' %}
  ```
Now, we need to specify the section and add the content in the section. 

**Here are some tips for working with inheritance:**

1. If you use {% extends %} in a template, it must be the first template tag in that template. Template inheritance won’t work, otherwise.

2. More {% block %} tags in your base templates are better. Remember, child templates don’t have to define all parent blocks, so you can fill in reasonable defaults in a number of blocks, then only define the ones you need later.

3. If you find yourself duplicating content in a number of templates, it probably means you should move that content to a {% block %} in a parent template.

4. If you need to get the content of the block from the parent template, the {{ block.super }} variable will do the trick. This is useful if you want to add to the contents of a parent block instead of completely overriding it. Data inserted using {{ block.super }} will not be automatically escaped, since it was already escaped, if necessary, in the parent template.

5. By using the same template name as you are inheriting from, {% extends %} can be used to inherit a template at the same time as overriding it. Combined with {{ block.super }}, this can be a powerful way to make small customizations.

We can also have our header, footer in the  differents template. To have header, footer in a different
templates, create new templates, add the code and include it in the base template.
  ```
  {% include 'path_of_template' %}
  ```
We can also have our css and javascript code in the base template and only html code in the other template(header, footer, etc...). 

