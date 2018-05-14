# Laravel Router

## REST
```php
Route::resource('user', 'UserController');
```

## Declaration
```php
Route::method('path', 'Controller@method');
```

### Rest
```php
Route::resource('user', 'UserController');
```

### Naming
```php
Route::get('/path', ['as' => 'name', 'use' => 'Controller@method']);
```

## Methods
```php
Route::get();
Route::post();
Route::patch();
Route::put();
Route::delete();
Route::any();
```

## Group
```php
Route::group(['prefix'] => 'home', function() {
  // ...Routes
});
```