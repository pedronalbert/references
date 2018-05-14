# Laravel Controller

```php
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