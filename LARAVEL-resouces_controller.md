# LARAVEL - Resource controller

Base controller: `php artisan make:controller <pascal-name>`

Resource controller: `php artisan make:controller <pascal-name>`

A resource controller is able to handle CRUD(create, read, update, delete) operations of a DB.

## Template:

```
<?php

namespace App\Http\Controllers;
use App\Comics;
use Illuminate\Http\Request;

class ComicsController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        //selects all data from DB and return an ouput page with retrived data
    }

    /**
     * Show the form for creating a new resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function create()
    {
        //returns a page with a form to create a new DB row  
    }

    /**
     * Store a newly created resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @return \Illuminate\Http\Response
     */
    public function store(Request $request)
    {
        //called by function create, stores form data into DB
    }

    /**
     * Display the specified resource.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function show(Comics $comic)
    {
        //returns an output page with data of 1 DB row
    }

    /**
     * Show the form for editing the specified resource.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function edit(Comics $comic)
    {
        //returns a page with a form to update 1 existing row
    }

    /**
     * Update the specified resource in storage.
     *
     * @param  \Illuminate\Http\Request  $request
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function update(Request $request, Comics $comic)
    {
        //called by edit, stores form data into DB
    }

    /**
     * Remove the specified resource from storage.
     *
     * @param  int  $id
     * @return \Illuminate\Http\Response
     */
    public function destroy(Comics $comic)
    {

    }
}
```

Best practice: create a subdirectory of /view with the name of the desired class
/comics
* /index.blade.php -> output all DB table data
* /create.blade.php -> form to create a new DB row
* /edit.blade.php -> form to update an existing DB row
* /show.blade.php -> output 1 specific DB row

## CREATE

### ComicsController.php create() /comics/create :

```
public function create()
{
    #/comics/create.blade.php
    return view('comics.create'); # form
}
```

### /view/comics/create.blade.php :

```
<form action="{{route('comics.store')}}" method="POST"> #send data to DB
    #checks that form data is from page form
    @csrf
    <div class="input-group mb-3">
        <span class="input-group-text" id="basic-addon2">Comics title</span>
        <input id="input-title" name="input-title" type="text" class="form-control" placeholder="Enter new comics title" >
     </div>

    <div class="input-group mb-3">
        <span class="input-group-text">Comics description</span>
        <textarea id="input-description" name="input-description" class="form-control" aria-label="With textarea"></textarea>
     </div>

    <div class="input-group mb-3">
        <span class="input-group-text" id="basic-addon2">Comics image thumb</span>
        <input id="input-thumb" name="input-thumb" type="text" class="form-control" placeholder="Enter new comics thumb" >
    </div>

    <div class="input-group mb-3">
        <span class="input-group-text">Comics price</span>
        <input id="input-price" name="input-price" type="number" class="form-control">
    </div>

    <div class="input-group mb-3">
        <span class="input-group-text" id="basic-addon2">Comics series</span>
        <input id="input-series" name="input-series" type="text" class="form-control" placeholder="Enter new comics series" >
     </div>

    <div class="input-group mb-3">
        <span class="input-group-text" id="basic-addon2">Comics type</span>
        <input id="input-type" name="input-type" type="text" class="form-control" placeholder="Enter new comics type" >
    </div>

    <div class="d-grid gap-2">
        <button class="btn btn-outline-primary" type="submit">Submit</button>
    </div>
</form>
```

### ComicsController.php store() :

```
public function store(Request $request)
{
    $data = $request->all();

    $newComics = new Comics;
    $newComics->c_title = $data['input-title'];
    $newComics->c_description = $data['input-description'];
    $newComics->c_thumb = $data['input-thumb'];
    $newComics->c_price = $data['input-price'];
    $newComics->c_series = $data['input-series'];
    $newComics->c_saledate = date('Y-m-d');
    $newComics->c_type = $data['input-type'];

    $newComics->save();

    return redirect()->route('comics.show', $newComics->id);
}
```

## READ

### ComicsController.php index() /comics : 

```
public function index()
{
    $comics = Comics::all();

    return view('comics.index', compact('comics'));
}
```

### ComicsController.php show() /comics/{id} :

```
public function show(Comics $comic)
{
    return view('comics.show', compact('comic'));
}
```

## UPDATE

### ComicsController.php edit() /comics/{id}/edit :

```
public function edit(Comics $comic)
{
    return view('comics.edit', compact('comic'));
}
```