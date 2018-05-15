# Laravel Validation
<!-- TOC -->

- [Laravel Validation](#laravel-validation)
  - [Request](#request)
  - [FormRequest](#formrequest)
    - [AfterHook](#afterhook)
    - [Authorization](#authorization)
    - [CustomMessages](#custommessages)
  - [Rules](#rules)
    - [Validating Arrays](#validating-arrays)
    - [Bail](#bail)
  - [Custom Rule](#custom-rule)
    - [Class Based](#class-based)
    - [Closure Based](#closure-based)
    - [Extend Validator](#extend-validator)

<!-- /TOC -->
## Request
All errors are bound on **$errors** variable on the view will be an instace of [Illuminate\Support\MessageBag](https://laravel.com/api/5.6/Illuminate/Contracts/Support/MessageBag.html)

```php
$request->validate(array $rules);
```

```html
@if ($errors->any())
  <div class="alert alert-danger">
    <ul>
      @foreach ($errors->all() as $error)
        <li>{{ $error }}</li>
      @endforeach
    </ul>
  </div>
@endif
```

## FormRequest
```sh
php artisan make:request MyFormPost
```
```php
namespace app\Http\Requests;

public function rules() {
  return array $rules;
}

/* controller */

namespace App\Http\Controllers;

public function store(MyFormPost $request) {
  $request->validated();
}
```

### AfterHook
The **$validator** is a instance of [Illuminate\Validation\Validator](https://laravel.com/api/5.6/Illuminate/Validation/Validator.html)

```php
namespace app\Http\Requests;

public function withValidator($validator) {
  $validator->after(function ($validator) {
    // ...
  });
}
```

### Authorization
```php
namespace app\Http\Requests;

public function authorize() {
  return boolean $authorized;
}
```

### CustomMessages
```php
namespace app\Http\Requests;

public function messages() {
  return [
    'title.required' => 'My message',
  ];
}
```


## Rules
[Rules](https://laravel.com/docs/5.6/validation#available-validation-rules)

### Validating Arrays
```php
$rules = [
  'person.profile' => string $rules,
  'person.*.email' => string $rules, 
];
```

### Bail
You can stop running validation runes on the first failure with **bail** rule

## Custom Rule

### Class Based
```sh
php artisan make:rule MyRule
```

```php
namespace App\Rules;

use Illuminate\Contracts\Validation\Rule;

class MyRule implements Rule {
  public function passes($attribute, $value) {
    return boolean;
  }

  public function message() {
    return string;
  }
}

// usage
$rules = [
  'title' => ['required', new MyRule],
];
```

### Closure Based
```php
$rules = [
  'title' => [
    'required',
    function($attribute, $value, $fail) {
      return $fail(string $message);
    }
  ]
]
```

### Extend Validator
```php
namespace App\Providers;

use Illuminate\Support\ServiceProvider;
use Illuminate\Support\Facades\Validator;

class AppServiceProvider extends ServiceProvider {
  public function boot() {
    Validator::extend('foo', $closure);
    Validator::extend('foo', 'Class@method');
  }
}
```