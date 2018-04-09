# Django Views
[Docs](https://docs.djangoproject.com/en/2.0/topics/http/views/#writing-views)
<!-- TOC -->

- [Django Views](#django-views)
  - [Function View](#function-view)
  - [Class View](#class-view)
    - [TemplateView](#templateview)
  - [Decorators](#decorators)
    - [Available Decorators](#available-decorators)

<!-- /TOC -->
## Function View
```python
from django.htto import JsonResponse

def hello_word(request):
  # return response
```
## Class View
```python
from dijango.views.generic import View

class HomeView(View):
  # Called on GET and POST
  def dispatch(self, request, *args, **kwargs)
    # return response
```

> When we use a class view we have to call the static method .as_view() for mount on router
```python
# urls.py
path('hello/', HomeView.as_view())
```

### TemplateView
 Render a template 
```python
from django.views.generic import TemplateView

class HomeView(TemplateView):
  template_name = 'users/home.html'
```

## Decorators
[Docs](https://docs.djangoproject.com/en/2.0/topics/http/decorators/#module-django.views.decorators.http)

```python
from django.views.decorators.http import require_http_methods

@require_http_methods(['GET', 'POST'])
def hello_view(request):
  pass
```

### Available Decorators
```python
require_GET()
require_POST()
require_safe()
```