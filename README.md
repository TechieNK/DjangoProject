# DjangoProject
## Day-2

## URL Routing
A URL is a uniform resource locator. It contains the address that links to a resource such as an HTML page.In Django, the premise is exactly the same. 
Inside each project is a `urls.py` file in the root directory. Django stores list of URLs in this file. Whenever a user types in the URL path, this file find 
the pattern that the user typed into the browser and return a page back to the user. Django based on whatever URL was matched, then triggers the function and 
the function returns back the page that the user is looking for.

To use the function:
  ```
    from django.http import HttpResponse
  ```
and define the function. Like 
  ```
    def home(request):
      return HttpResponse("Home page")
    def contact(request):
      return HttpResponse("Contact page")
  ```
In the above function, the function returns the string. And in the `urlspattern` we need to create a path and and call the function.
  ```
    path('',home),
    path('about/',contacts)
  ```

We can also make the function to return API data like a JSON response and the HTTP response.
