# Django Test
## Boilerplate
```python
from django.test import TestCase

class SmokeTest(TestCase):
  def test_method():
    pass
```

## Assertions
```pyton
assertTemplateUsed(response, 'home.html')
```

## Views
### Requests
```python
self.client.get(url)
self.client.post(url, data={...})
```

## LiveServerTestCase
Create a clean database and start up a development server