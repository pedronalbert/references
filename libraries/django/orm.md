# Django ORM
<!-- TOC -->

- [Django ORM](#django-orm)
  - [Retrieving Results](#retrieving-results)
    - [Methods](#methods)
      - [Relationship](#relationship)
      - [Chaining](#chaining)
      - [Ordering](#ordering)
      - [Limiting](#limiting)
    - [FieldLookups](#fieldlookups)
  - [Creating](#creating)
  - [Relationship](#relationship-1)

<!-- /TOC -->
## Retrieving Results
> For retrieveng results we use Model.objects.[method]
### Methods
```python
# Return QuerySet
.all()
.filter(**field_lookups)
.exclude(**field_lookups)
.first()

# Return Plain
.get(**field_lookups)

```

#### Relationship
[Docs](https://docs.djangoproject.com/en/2.0/topics/db/queries/#lookups-that-span-relationships)

You can query relationship with **entry__[relation_field]__[field_lookup]**

#### Chaining
```py
.filter(
  **kwarts
).exclude(
  **kwarts
)
```

#### Ordering
```py
QuerySet.order_by('foo)
```

#### Limiting
```py
QuerySet[1:5]
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