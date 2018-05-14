# Laravel Blade

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