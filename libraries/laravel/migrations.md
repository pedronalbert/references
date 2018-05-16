# Laravel Migrations

## Definition
```sh
php artisan make:migration create_users_table
```

```php
use Illuminate\Support\Facades\Schema;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Database\Migrations\Migration;

class CreateUsersTable extends Migration {
  public function up() {
    // ...
  }

  public function down() {
    // ...
  }
}
```

### Tables
```php
Schema::create('users', function (BluePrint, $t) {
  // ...
});
Schema::hasTable('users');
Schema::hasColumn('users', 'email');
Schema::rename('from', 'to');
Sceham::drop('users');
Schema::dropIfExists('users');
```

### Columns
#### Types
[Types](https://laravel.com/docs/5.6/migrations#columnse)

#### Modifies
[Modifiers](https://laravel.com/docs/5.6/migrations#columnse)

#### Modify
```php
$t->renameColumn('from', 'to');
$t->dropColumn('first_name');
$t->dropColumn(['first_name', 'last_name']);
```

### Indexes
```php
$t->primary(string $name);
$t->unique(string $column, string $indexName?);
$t->index(['email', 'dni']);

// drop
$t->dropPrimary(string $name);
$t->dropUnique(string $name);
$t->dropIndex(string $name);
```

### ForeignKey
```php
$t->foreign(string $column)->references(string $foreign_column)->on(string $table);
$t->dropForeign(string $name)
```

## Commands
```sh
php artisan make:migration create_users_table
php artisan migrate
php artisan migrate:rollback --step=2
php artisan migrate:reset
php artisan migrate:refresh --seed
```