# Laravel Blade

## Binding
```html
{{ $bar }}
```

### JSON
```html
@json($content)
```

### Escape Curly
```html
@{{ content }}

@verbatim
  {{ content }}
@endverbatim
```

## Inheritance
```html
<!-- base.blade.php -->
<html>
  <head>
    <title>@yield('title')</title>
  </head>
  <body>
    @section('sidebar')
      Default Content
    @show

    @yield('content')
  </body>
</html>

<!-- child.blade.php -->
@extends('base')

@section('sidebar')
  @parent

  <p>Other Content</p>
@endsection

@section('content')
  <p>Content</p>
@endsection
```

## Components & Slots
```html
<!-- my_component.blade.php -->
<div>
  {{ $slot }}
</div>

<!-- list.blade.php -->
@component('my_component')
  <p>I'm the content</p>
@endcomponent
```

### Multiple
```html
<!-- my_component.blade.php -->
<div>
  <h1>{{ $title }}</h1>

  {{ $slot }}
</div>

<!-- list.blade.php -->
@component('my_component')
  @slot('title')
    I'm the title
  @endslot

  <p>I'm the content</p>
@endcomponent
```

### Params
```html
<!-- list.blade.php -->
@component('my_component', ['foo' => 'bar'])
  <p>I'm the content</p>
@endcomponent
```

### Aliasing
Should be place in the **boot** method of your **AppServiceProvider**

```php
use Illuminate\Support\Facades\Blade;

Blade::component('components.alert', 'alert');
```

```html
@alert
  Alert Content
@endalert
```

## Include
```html
@include('view.name', ['foo' => 'bar'])
@includeWhen(boolean, 'view'name, ['foo' => 'bar'])
```

## Stacks
```html
<head>
  @stack('scripts')
</head>

@push('scripts')
  ...
@endpush

@prepend('scripts')
  ...
@endpush
```

## Control Flow

### Conditional

#### If
```html
@if ()
  ...
@elseif ()
  ...
@else
  ...
@endif
```

#### Unless

```html
@unless ()
  ...
@endunless
```

#### Isset & Empty
```html
@isset()
  ...
@endisset

@empty()
  ...
@endempty
```

#### Auth & Guest
```html
@auth
  ...
@endauth

@guest
  ...
@endguest
```

##### AuthGuard
```html
@auth('admin')
  ...
@endauth

@guest('admin')
  ...
@endguest
```

#### Section
```html
@hasSection('navigation')
  <div>
    @yield('navigation')
  </div>
@endif
```

#### Switch
```html
@switch($var)
  @case(1)
    ...
    @break

  @default
    ...
@endswitch
```

### Loops
#### For
```html
@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}
@endfor
```

#### Foreach
```html
@foreach ($users as $user)
    <p>This is user {{ $user->id }}</p>
@endforeach
```

#### For
```html
@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}
@endfor
```

#### Forelse
```html
@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse
```

#### While
```html
@while (true)
    <p>I'm looping forever.</p>
@endwhile
```

#### Helpers
```html
@continue
@continue(condition)

@break
@break(condition)

$loop->index
$loop->iteration
$loop->remaining
$loop->count
$loop->first
$loop->last
$loop->depth
$loop->parent
```

## PHP
```html
@php
  ...
@endphp
```

## Service
The @inject directive may be used to retrieve a service from the Laravel service container. The first argument passed to @inject is the name of the variable the service will be placed into, while the second argument is the class or interface name of the service you wish to resolve.

```html
@inject('metrics', 'App\Services\MetricsService')

<div>
  {{ $metrics->foo() }}
</div>
```

## Custom Directive
Should be place in the **boot** method of your **AppServiceProvider**
```php
use Illuminate\Support\Facades\Blade;

Blade::directive('foo', function ($expression) {
  return '<?php echo ($expression) ?>';
});
```