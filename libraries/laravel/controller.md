# Laravel Controller

```php
namespace App\Http\Controllers;

use App\Http\Controllers\Controller;

class MyController extends Controller {
  // ...methods
}
```

## Parameters
```php
class MyController extends Controller {
  public function method($bar, $cat) {
    // ...
  }
}
```

## Middleware
```php
class MyController extends Controller {
  public function __construct() {
    $this->middleware('foo');
    $this->middleware('foo')->only('index');
    $this->middleware('foo')->except('store');
  }
}
```

## Dependency Injection
```php
class MyController extends Controller {
  protected $users;

  public function __construct(UserRepository $user) {
    $this->users = $users;
  }
}
```

## REST
```sh
php artisan make:controller MyController --resource
```

```php
class MyController extends Controller {
  public function index() {
    // ...
  }

  public function create() {
    // ...
  }

  public function store($) {
    // ...
  }

  public function show() {
    // ...
  }

  public function edit() {
    // ...
  }

  public function update() {
    // ...
  }

  public function destroy() {
    // ...
  }
}
```

## Request
[API](https://laravel.com/api/5.6/Illuminate/Http/Request.html)
```php
use Illuminate\Http\Request;

class MyController extends Controller {
  public function method(Request $request, $arg) {
    // ...
  }
}
```

### POST params
```php
$request->all();
$request->input(string $key, string|array $default = null);
$request->only(array $key);
$request->except(array $key);
$request->has(string|array $key);

// Access to JSON & Arrays
$request->input('foo.0.name');
$request->input('foo.bar');
```

### GET params
```php
$request->query($name, $defaultValue?);
```

## Response
### View
```php
response()->view(string $name, array $data?, integer $statusCode);
view(string $name, array $data?, integer $status?);
```

### Json
```php
response()->json(array $data)
```

### Redirect
```php
redirect('/path');
redirect()->route(string $name, array $data?);
redirect()->action('Controller@method', array $data?);
```

### Macro
```php
<?php

namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Support\Facades\Response;

class ResponseMacroServiceProvider extends ServiceProvider
{
    public function boot()
    {
        Response::macro('caps', function ($value) {
            return Response::make(strtoupper($value));
        });
    }
}

// usage
response()->caps('foo');
```