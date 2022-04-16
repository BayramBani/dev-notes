# Laravel CRUD
---

## Installation

> via composer

````shell
composer create-project laravel/laravel webapp
````

> via Laravel installer

````shell
composer global require laravel/installer
laravel new webapp
````

## Database configuration

> /.env

````tex
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_starter
DB_USERNAME=root
DB_PASSWORD=
````

> migrate database

````
php artisan migrate
````

## Starter Kits (Laravel Breeze)

> Laravel Breeze is a minimal, simple implementation of all of Laravel's authentication features

````shell
composer require laravel/breeze --dev
php artisan breeze:install
npm install
npm run dev
php artisan migrate
````

## Create model and migrations

````shell
php artisan make:model Contact -m
````

> Model : /app/Models/Contact.php

````php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;

class Contact extends Model
{
    use HasFactory;
    
    protected $fillable = ['name', 'email', 'phone', 'address'];
}

````

> Migration : /database/migrations/{date}_create_contacts_table.php

````php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

class CreateContactsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('contacts', function (Blueprint $table) {
            $table->id();
            $table->string('name');
            $table->string('email');
            $table->string('phone')->nullable();
            $table->string('address')->nullable();
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
        Schema::dropIfExists('contacts');
    }
}

````

````shell
php artisan migrate
````

## Create controller

````shell
php artisan make:controller ContactController --resource --model=Contact
````

> Controller :  /app/Http/Controllers/ContactController.php

````php
<?php

namespace App\Http\Controllers;

use App\Models\Contact;
use Illuminate\Http\Request;

class ContactController extends Controller
{
    /**
     * Display a listing of the resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function index()
    {
        $contacts = Contact::all();
        return view('contacts.index', compact('contacts'));
    }

    /**
     * Show the form for creating a new resource.
     *
     * @return \Illuminate\Http\Response
     */
    public function create()
    {
        return view('contacts.create');
    }

    /**
     * Store a newly created resource in storage.
     *
     * @param  \Illuminate\Http\Request $request
     * @return \Illuminate\Http\Response
     */
    public function store(Request $request)
    {
        $request->validate([
            'name' => 'required',
            'email' => 'required',
        ]);
        Contact::create($request->all());
        return redirect()->route('contacts.index');
    }

    /**
     * Display the specified resource.
     *
     * @param  \App\Models\Contact $contact
     * @return \Illuminate\Http\Response
     */
    public function show(Contact $contact)
    {
        return view('contacts.show', compact('contact'));
    }

    /**
     * Show the form for editing the specified resource.
     *
     * @param  \App\Models\Contact $contact
     * @return \Illuminate\Http\Response
     */
    public function edit(Contact $contact)
    {
        return view('contacts.edit', compact('contact'));
    }

    /**
     * Update the specified resource in storage.
     *
     * @param  \Illuminate\Http\Request $request
     * @param  \App\Models\Contact $contact
     * @return \Illuminate\Http\Response
     */
    public function update(Request $request, Contact $contact)
    {
        $request->validate([
            'name' => 'required',
            'email' => 'required',
        ]);
        $contact->update($request->all());
        return redirect()->route('contacts.index');
    }

    /**
     * Remove the specified resource from storage.
     *
     * @param  \App\Models\Contact $contact
     * @return \Illuminate\Http\Response
     */
    public function destroy(Contact $contact)
    {
        $contact->delete();
        return redirect()->route('contacts.index');
    }
}

````

## Create views

1.  `/resources/views/contacts/layout.blade.php`

````php
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport"
        content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Laravel Basic CRUD</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
</head>
<body>
<div class="container">
  @yield('content')
</div>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj"
        crossorigin="anonymous"></script>
</body>
</html>
````

2. `/resources/views/contacts/index.blade.php`

````php
@extends('contacts.layout')

@section('content')
  <div class="row">
    <div class="col-12">
      <h1 class="display-4">Contact List</h1>
      <hr>
    </div>
    <div class="col-12 mt-2">
      <a class="btn btn-sm btn-primary" href="{{ route('contacts.create') }}">add</a>
      <hr>
    </div>
  </div>
  <div class="row">
    <div class="col">
      <table class="table">
        <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">Email</th>
          <th scope="col">Phone</th>
          <th scope="col">Address</th>
          <th scope="col">Action</th>
        </tr>
        </thead>
        <tbody>
        @foreach($contacts as $contact)
          <tr>
            <td>{{$contact->id}}</td>
            <td>{{$contact->name}}</td>
            <td>{{$contact->email}}</td>
            <td>{{$contact->phone}}</td>
            <td>{{$contact->address}}</td>
            <td>
              <form action="{{route('contacts.destroy', $contact->id)}}" method="POST">
                <a class="btn btn-sm btn-secondary"
                   href="{{route('contacts.show',$contact->id)}}">show</a>
                <a class="btn btn-sm btn-success"
                   href="{{route('contacts.edit',$contact->id)}}">edit</a>
                @csrf
                @method('DELETE')
                <button type="submit" class="btn btn-sm btn-danger">delete</button>
              </form>
            </td>
          </tr>
        @endforeach
        </tbody>
      </table>
    </div>
  </div>
@endsection
````

3. `/resources/views/contacts/create.blade.php`

````php
@extends('contacts.layout')

@section('content')
  <div class="row">
    <div class="col-12">
      <h1 class="display-4">Add New Contact</h1>
      <hr>
    </div>
    <div class="col-12">
      <a class="btn btn-sm btn-secondary" href="{{route('contacts.index')}}">back</a>
      <hr>
    </div>
  </div>

  @if ($errors->any())
    <div class="row">
      <div class="col">
        <ul>
          @foreach($errors->all() as $error)
            <li>{{$error}}</li>
          @endforeach
        </ul>
      </div>
    </div>
  @endif

  <div class="row">
    <div class="col">
      <form action="{{route('contacts.store')}}" method="post">
        @csrf
        <div class="mb-3">
          <label for="name" class="form-label">Name</label>
          <input name="name" type="text" class="form-control form-control-sm" required/>
        </div>
        <div class="mb-3">
          <label for="email" class="form-label">Email</label>
          <input name="email" type="email" class="form-control form-control-sm" required/>
        </div>
        <div class="mb-3">
          <label for="phone" class="form-label">Phone</label>
          <input name="phone" type="tel" class="form-control form-control-sm"/>
        </div>
        <div class="mb-3">
          <label for="name" class="form-label">Address</label>
          <input name="address" type="text" class="form-control form-control-sm"/>
        </div>
        <div class="mb-3">
          <button type="submit" class="btn btn-sm btn-primary">save</button>
        </div>
      </form>
    </div>
  </div>
@endsection
````

4. `/resources/views/contacts/edit.blade.php`

````php
@extends('contacts.layout')

@section('content')
  <div class="row">
    <div class="col-12">
      <h1 class="display-4">Edit Contact</h1>
      <hr>
    </div>
    <div class="col-12">
      <a class="btn btn-sm btn-secondary" href="{{route('contacts.index')}}">back</a>
      <hr>
    </div>
  </div>

  @if ($errors->any())
    <div class="row">
      <div class="col">
        <ul>
          @foreach($errors->all() as $error)
            <li>{{$error}}</li>
          @endforeach
        </ul>
      </div>
    </div>
  @endif

  <div class="row">
    <div class="col">
      <form action="{{route('contacts.update', $contact->id)}}" method="post">
        @csrf
        @method('PUT')
        <div class="mb-3">
          <label for="name" class="form-label">Name</label>
          <input name="name" type="text" class="form-control form-control-sm" value="{{ $contact->name }}" required/>
        </div>
        <div class="mb-3">
          <label for="email" class="form-label">Email</label>
          <input name="email" type="email" class="form-control form-control-sm" value="{{ $contact->email }}" required/>
        </div>
        <div class="mb-3">
          <label for="phone" class="form-label">Phone</label>
          <input name="phone" type="tel" class="form-control form-control-sm" value="{{ $contact->phone }}"/>
        </div>
        <div class="mb-3">
          <label for="name" class="form-label">Address</label>
          <input name="address" type="text" class="form-control form-control-sm" value="{{ $contact->address }}"/>
        </div>
        <div class="mb-3">
          <button type="submit" class="btn btn-sm btn-primary">save</button>
        </div>
      </form>
    </div>
  </div>

@endsection
````

5. `/resources/views/contacts/show.blade.php`

````php
@extends('contacts.layout')

@section('content')
  <div class="row">
    <div class="col-12">
      <h1 class="display-4">Contact</h1>
      <hr>
    </div>
    <div class="col-12 mt-2">
      <a class="btn btn-sm btn-secondary" href="{{ route('contacts.index') }}">back</a>
    </div>
  </div>
  <div class="row">
    <div class="col">
      <table class="table">
        <tbody>
        <tr>
          <td>#</td>
          <td>{{$contact->id}}</td>
        </tr>
        <tr>
          <td>Name</td>
          <td>{{$contact->name}}</td>
        </tr>
        <tr>
          <td>Email</td>
          <td>{{$contact->email}}</td>
        </tr>
        <tr>
          <td>Phone</td>
          <td>{{$contact->phone}}</td>
        </tr>
        <tr>
          <td>Address</td>
          <td>{{$contact->address}}</td>
        </tr>
        </tbody>
      </table>
    </div>
  </div>
@endsection
````

## Create routes

> /routes/web.php

````php
use App\Http\Controllers\ContactController;
// {***} ///
Route::resource('contacts', ContactController::class);
````

## Serve

````shell
php artisan serve
````

> navigate to : http://127.0.0.1:8000/contacts







---

# Errors

`SQLSTATE[42000]: Syntax error or access violation: 1071 La clé est trop longue`

> `/app/Providers/AppServiceProvider.php`

````php
use Illuminate\Database\Schema\Builder;
// ...
public function boot() {
	Builder::defaultStringLength(191);
}
````
