# Laravel Services

## Share View Data
```php
namespace App\Providers;

use Illuminate\Support\Facades\View;

class AppServiceProvider extends ServiceProvider {
    public function boot() {
        View::share('key', 'value');
    }

    public function register() {
        //
    }
}
```

## View Composer
[Docs](https://laravel.com/docs/5.6/views#view-composers)

To Read