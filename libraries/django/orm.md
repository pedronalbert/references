# Django ORM
<!-- TOC -->

- [Django ORM](#django-orm)
  - [Retrieving Results](#retrieving-results)
    - [Methods](#methods)
    - [FieldLookups](#fieldlookups)
  - [Creating](#creating)
  - [Relationship](#relationship)

<!-- /TOC -->
## Retrieving Results
> For retrieveng results we use Model.objects.[method]
### Methods
```python
.get(...fields)
.filter(...fieldLookups)
.all()
.first()
```

### FieldLookups
> FieldLookups are builded with fieldName__lookup
```python
__exact
__iexact
__contains
__icontains
__in # Array
__gt
__gte
__lt
__lte
__startswith
__istartswith
__endswith
__iendswith
__range # Tuple
__date # datetime.date
__date__[year|month|day|week|week_day]__[gt|gte|lt|lte]
__time # datetime.time
__hour
__minute
__second
__isnull # Boolean
__regex # RegEx
__iregex # RegEx
```

## Creating
```python
User.objcets.create(first_name = "Pepe")
```

## Relationship
> All related methoud must be used over a related entity ex: Users.posts

```python
.add(objs)
.create(objs)
.remove(objs)
.clear()
```