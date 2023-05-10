# LARAVEL - Model & Controller

## Model

Create a new model who represent the table movie

```
php artisan make:model Movie// ! PascalCase singular
```

## Controller

Create a new controller for queries:

```
php artisan make:controller <ControllerName> // ! PascalCase singular
```
Controller example code:
```
<?php

namespace App\Http\Controllers;
# !! import the created model of the table Movie
use App\Movie;
use Illuminate\Http\Request;

class DefaultController extends Controller
{
    public function index(){
        # operations

        #query SELECT * FROM movie
        $movies = Movie::all();

        # return statement like web.php with DB data as parameter 
        return view("index",[
            "movies" => $movies
        ]);
    }
}

```

### Assign a routes/web.php route to the controller

```
# send route to <controller name>@<method>
Route::get('/', 'DefaultController@index');
```