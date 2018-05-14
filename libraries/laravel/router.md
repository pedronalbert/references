# Laravel Router
<!-- TOC -->

- [Laravel Router](#laravel-router)
  - [Declaration](#declaration)
    - [REST](#rest)
    - [Naming](#naming)
    - [Redirects](#redirects)
    - [View](#view)
  - [Methods](#methods)
  - [Group](#group)
    - [Middleware](#middleware)
    - [Namespacing](#namespacing)
    - [Prefixing](#prefixing)
  - [Params](#params)
    - [Optional](#optional)
    - [Constraint](#constraint)

<!-- /TOC -->

## Declaration
```php
Route::method('path', 'Controller@method');
```

### REST
```php 
 Route::resource('user', 'UserController');
```

### Naming
```php
Route::method('/path', $closure)->name('foo');
```

### Redirects
```php
Route::redirect('/from', '/to', 301);
```

### View
```php
Route::view('/path', 'view_name');
Route::view('/path', 'view_name', ['foo' => 'bar']);
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

### Middleware
```php
Route::middleware(['one', 'two'])->group(function () {
  // ...Routes
}):
```

### Namespacing
```php
Route::namespace('Admin')->group(function () {
  // Controllers within 'App\Http\Controllers\Admin' namespace
});
```

### Prefixing
```php
Route::prefix('admin')->group(function () {
  // routes starting with '/admin'
});
```

## Params
```php
Route::method('/path/{bar}', $closure);
Route::method('/path/{bar}', 'Controller@method');
```

### Optional
```php
Route::method('/path/{bar?}');
```

### Constraint
```php
Route::method('/path/{foo}', $closure)->where(['foo' => '[0-9]']);
```
