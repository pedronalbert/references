# Django Router

## Basic Path
```python
from django.urls import path

urlpatterns = [
  path('home/', views.home),
]
```

## Parameters
```python
urlpatterns = [
  path('users/<int:user_id>/', views.show_user),
]
```

### Default Parameters
```python
urlpatterns = [
  path('users/<int:user_id>/', views.show_user, {'foo': 'bar'}),
]
```

### Available Types
```python
str
int
slug
uuid
path
```

### Custom Type
You have to define
- A regex
- A to_python(self, value)
- to_url(self, value)
- Register converter

```python
class FourDigitYearConverter:
  regex = '[0-9]{4}'

  def to_python(self, value):
    return int(value)

  def to_url(self, value):
    return '%04d' % value

# urls.py
from django.urls import register_converter

register_converter(FourDigitYearConverter, 'converter_name')
```

## Regex Path
```python
from django.urls import re_path

urlpatterns = [
  re_path(r'^articles/(?P<year>[0-9]{4})/$', views.year_archive),
]
```

## Include
```python
from django.urls import include, path

urlpatterns = [
  path('community/', include('aggregator.urls')),
  path('contact/', include('contact.urls')),
]
```