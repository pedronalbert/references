# Laravel Orm

## Model
```sh
php artisan make:model Flight --migration
```

```php
use Illuminate\Database\Eloquent\Model;

class Flight extends Model {
  protected $table = 'table_name';
}
```

### Relationship
#### One To One
```php
class Post extends Model {
  public function user() {
    return $this->hasOne('App\User', string $foriengKey?, string $localKey);
  }
}
```

#### One To Many
```php
class Post extends Model {
  public function comments() {
    return $this->hasMany('App\Comment', string $foreignKey? string $localKey?);
  }
}
```

#### Through
```php
class Person extends Model {
  // ...
}

class Grouop extends Model {
  public function members() {
    return $this->hasManyThrough('Person', 'Membership');
  }
}

class Membership extends Model {
  public function person() {
    return $this->belongsTo('Person');
  }

  public function group() {
    return $this->belongsTo('Group');
  }
}
```

#### Belongs To
```php
class Comment extends Model {
  public function post() {
    return $this->belongsTo('App\Post', string $foreignKey?);
  }
}
```

#### Belongs To Many
```php
class User extends Model {
  public function roles() {
    return $this->belongsToMany('App\Role');
  }
}
```

## Query
### Return QueryBuilder
```php
Entity::where(string $name, mixed $value)

// Modifiers
->orderBy(string $field, string 'asc|desc');
->take(integer $amount);

// Retrieing
->get();
->max(string $field);
->count();
->first();
->firstOrFail();
```

### Return Plain
```php
Entity::all();
Entity::find($pk);
Entity::find(array $pks);
Entity::findOrFail(array $pks);
```

### Iteration

#### Chunk
```php
User::chink(200, function ($users) {
  foreach ($users as $user) {
    // ...
  }
});
```

#### Cursors
```php
foreach (User::where()->cursor() as $user) {
  // ...
}
```

## Creating
> When you use create you need to specify **fillable** fields on model
```php
User::create(array $attrs);
User::firstOrCreate(array $attrs)
User::firstOrNew(array $attrs)
```

## Updating
```php
$users->update(array $attributes);

User::updateOrCreate(array $attrs);
```

## Deleting
```php
User::destroy($pk)

$query->delete();
```