# Laravel Middleware
<!-- TOC -->

- [Laravel Middleware](#laravel-middleware)
  - [Probando](#probando)

## Definition
```sh
php artisan make:middleware MyMiddleware
```
```php
namespace App\Http\Middleware;

use Closure;
[Illuminate\Http\Request](https://laravel.com/api/5.6/Illuminate/Http/Request.html)

class MyMiddleware {
  public function handle($request, Closure $next) {
    // ...Before
    $response = $next($request);

    // ...After

    return $response;
  }
}
```

## Terminate
Sometimes a middleware may need to do some work after the HTTP response has been prepared. For example, the "session" middleware included with Laravel writes the session data to storage after the response has been fully prepared. If you define a terminate method on your middleware, it will automatically be called after the response is ready to be sent to the browser.

```php
class MyMiddleware {
  public function terminate($request, $response) {
    // ...
  }
}
```

## Register
```php
namespace App\Http\Kernel;

protected $routeMiddleware = [
  'foo' => \App\Http\Middleware::class,
];
```