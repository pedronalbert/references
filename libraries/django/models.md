# Django Models
<!-- TOC -->

- [Django Models](#django-models)
  - [FieldTypes](#fieldtypes)
  - [FieldOptions](#fieldoptions)
  - [Inheritance](#inheritance)
    - [Abstract Models](#abstract-models)
    - [MultiTable Inheritance](#multitable-inheritance)
    - [ProxyModel](#proxymodel)
  - [RelationShips](#relationships)
    - [HasOne](#hasone)
    - [ManyToMany](#manytomany)
    - [Through](#through)
  - [Migrations](#migrations)
    - [RunPython](#runpython)

<!-- /TOC -->
```python
from django.db import models

class User(models.Model):
  first_name = models.CharField(...opts)
```

## FieldTypes
[Docs](https://docs.djangoproject.com/en/2.0/ref/models/fields/#field-types)
```python
AutoField(...opts)
BigAutoField(...opts)
BigIntegerField(...opts)
BinaryField(...opts)
BooleanField(...opts)
CharField(...opts)
DateField(...opts)
DateTimeField(...opts)
DecimalField(...opts)
DurationField(...opts)
EmailField(...opts)
FileField(...opts)
FloatField(...opts)
ImageField(...opts)
IntegerField(...opts)
GenericIPAddressField(...opts)
NullBooleanField(...opts)
PositiveIntegerField(...opts)
PositiveSmallIntegerField(...opts)
SlugField(...opts)
SmallIntegerField(...opts)
TextField(...opts)
TimeField(...opts)
URLField(...opts)
UUIDField(...opts)
```

## FieldOptions
[Docs](https://docs.djangoproject.com/en/2.0/ref/models/fields/)
```python
# General
null = Boolean
blank = Boolean
choices = (
  ('fr', 'France'),
  ('es', 'Spain')
)
default = String
editable = Boolean
primary_key = Boolean
unique = Boolean
db_column = String
db_index = Boolean
db_tablespace = String
```

## Inheritance

### Abstract Models
> Used when you want to put common fields in other models
```python
class CommonInfo(models.Model):
  name = models.CharField()

  class Meta:
    abstract = True

class User(CommonInfo):
  pass
```

### MultiTable Inheritance
[Docs](https://docs.djangoproject.com/en/2.0/topics/db/models/#multi-table-inheritance)

```python
from django.db import models

class Place(models.Model):
  name = models.CharField(max_length=50)

class Restaurant(Place):
  serves_pizza = models.BooleanField(default=False)
```

### ProxyModel
> Add model behaviours without alter the base class
```python
from django.db import models

class Person(models.Model):
  first_name = models.CharField(max_length=30)
  last_name = models.CharField(max_length=30)

class User(Person):
  class Meta:
    proxy = True
  
  @property
  def full_name(self):
    return self.first_name + ' ' + self.last_name
```
## RelationShips

### HasOne
> We only need to specify the belongs_to field and we will have bidirectional relations
```python
from django.db import models

class User(models.Model):
  first_name = models.CharField(opts)

class Post(models.Model):
  user = models.ForeignKey(User)
```

### ManyToMany
```python
from django.db import models

class Topping(models.Model):
  # ...

class Pizza(models.Model):
  toppings = models.ManyToManyField(Topping)
```

### Through
```python
from django.db import models

class Person(models.Model):
  name = models.CharField()

class Group(models.Model):
  members = models.ManyToManyField(Person, through='Membership')

class Membership(models.Model):
  person = models.ForeignKey(Person, on_delete=models.CASCADE)
  group = models.ForeignKey(Group, on_delete=models.CASCADE)

```

## Migrations

### RunPython
You can run Python script on migrations with RunPython method
```python
from django.db import migrations

def combine_names(apps, schema_editor):
    # We can't import the Person model directly as it may be a newer
    # version than this migration expects. We use the historical version.
    Person = apps.get_model('appname', 'Person')
    for person in Person.objects.all():
        person.name = '%s %s' % (person.first_name, person.last_name)
        person.save()

class Migration(migrations.Migration):

    dependencies = [
        ('appname', '0001_initial'),
    ]

    operations = [
        migrations.RunPython(combine_names),
    ]
```

> If you use models from another app you have to specifity the last dependency of that app
```python
class Migration(migrations.Migration):
  dependencies = [
    ('app1', '0001_initial'),
    ('app2', '0004_foobar')
  ]
```