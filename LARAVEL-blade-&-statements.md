# LARAVEL- conditions, loops, layouts

## BLADE PHP TEMPLATE ENGINE

Blade is the Laravel official template engine and makes PHP easier to write using directives preceded by @  

### Display data
 
```
<h1> Hello, {{ $phpVariable }} </h1>
```

### PHP Statement

```
@php
    $isActive = false;
    $hasError = true;
@endphp
```

### IF Statements

```
@if (count($records) === 1)
    I have one record!
@elseif (count($records) > 1)
    I have multiple records!
@else
    I don't have any records!
@endif
```

### UNLESS Statements

Unless a condition is verified:

```
@unless (Auth::check())
    You are not signed in.
@endunless
```

### ISSET & EMPTY Statements

```
@isset($records)
    // $records is defined and is not null...
@endisset

@empty($records)
    // $records is "empty"...
@endempty
```

### AUTHENTICATION Statements

Determine if a user is authenticated or guest

```
@auth
    // The user is authenticated...
@endauth

@guest
    // The user is not authenticated...
@endguest
```

### ENVIROMENT Statements

Specify if an application is running in production/development, additionally you can create new enviroments:

```
@production
    // Production specific content...
@endproduction

@env('staging')
    // The application is running in "staging"...
@endenv

@env(['staging', 'production'])
    // The application is running in "staging" or "production"...
@endenv
```

### SWITCH Statements

```
@switch($i)
    @case(1)
        First case...
        @break

    @case(2)
        Second case...
        @break

    @default
        Default case...
@endswitch
```

### LOOPS Statements

```
@for ($i = 0; $i < 10; $i++)
    The current value is {{ $i }}
@endfor

@foreach ($users as $user)
    <p>This is user {{ $user->id }}</p>
@endforeach

@forelse ($users as $user)
    <li>{{ $user->name }}</li>
@empty
    <p>No users</p>
@endforelse

@while (true)
    <p>I'm looping forever.</p>
@endwhile

@foreach ($users as $user)
    @if ($loop->first)
        This is the first iteration.
    @endif

    @if ($loop->last)
        This is the last iteration.
    @endif

    <p>This is user {{ $user->id }}</p>
@endforeach

@foreach ($users as $user)
    @foreach ($user->posts as $post)
        @if ($loop->parent->first)
            This is the first iteration of the parent loop.
        @endif
    @endforeach
@endforeach
```

### INCLUDE Statements

```
@include('shared.errors') //directory.file
```