#   LARAVEL - Migrations & Seeders

## Migrations

Migrations are DB tables blueprints.
Once you migrate a migration, Laravel creates table on DB from the blueprint

Create a new migration:

```
php artisan make:migration create_<table_name>_table
```

/database/migrations/2022_01_10_130433_create_<table_name>_table.php :
```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTravelpackagesTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        # Define table schema
        Schema::create('TravelPackages', function (Blueprint $table) {
            $table->bigIncrements('tp_id'); #auto increment field
            $table->string('tp_name');#string field
            $table->string('tp_locations');#enum field with options all countries in config/_countryesArray.php
            $table->float('tp_price');#float field
            $table->string('tp_description');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('TravelPackages');
    }
}
```

Method up() gets executed on migration.
Method down() gets executed on migration:rollback.

Create table on DB:

```
php artisan migrate
```

Undo table creation on DB

```
php artisan migrate:rollback
```

Update table:

```
php artisan make:migration update_<table-name>_table --table=<table_to_be_updated>
```

Delete all migrations:

```
php artisan migrate:reset
```

## Seeders

Seeders are used to quickly populate a DB with fake data using Faker PHP class.

Create a new seeder:

```
php artisan make:seeder UsersTableSeeder
```

install Faker class:

```
composer remove fzaninotto/faker
composer require fakerphp/faker
```

/database/seeds/<seed_name>.php:

```
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateTravelpackagesTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('TravelPackages', function (Blueprint $table) {
            $table->bigIncrements('tp_id'); #auto increment field
            $table->string('tp_name');#string field
            $table->string('tp_locations');#enum field with options all countries in config/_countryesArray.php
            $table->float('tp_price');#float field
            $table->string('tp_description');
            $table->timestamps();
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('TravelPackages');
    }
}
```

