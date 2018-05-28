# Apiato

## Caveats
- Al usar un DataTransporter no toma los parametros de la url como `id` el cual se debe meter explicitamente
```php
$transporter = new DataTransporter($request);
$transporter->id = $request->id;
```