# DjangoProject
## Day-3 

## Templates
A template is a text file. It can generate any text-based format (HTML, XML, CSV, etc.).
A template contains variables, which get replaced with values when the template is evaluated, and tags, which control the logic of the template.

Our templates needs to be stored in app_folder-> templates-> app_name-> template_name.html. To display that template using function we can use `render() method`. 
  ```
  def home(request):
    return render(request, 'accounts/dashboard.html')
  ```
Here, accounts is the name of the directory in templates directory where our templates are present.
