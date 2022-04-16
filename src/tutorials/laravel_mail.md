# Laravel Mail
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

## Mail configuration

> /.env

````tex
MAIL_MAILER=smtp
MAIL_HOST=smtp.gmail.com
MAIL_PORT=587
MAIL_USERNAME=<your-username@gmail.com>
MAIL_PASSWORD=<your-password>
MAIL_ENCRYPTION=tls
MAIL_FROM_ADDRESS=<you@email.com>
MAIL_FROM_NAME="${APP_NAME}"
````
## Generating Mailables

````shell
php artisan make:mail Message
````

with markdown

````shell
php artisan make:mail Message --markdown=emails.message
````

> Maillable: /app/Mail/Message.php

````php
<?php

namespace App\Mail;

use Illuminate\Bus\Queueable;
use Illuminate\Contracts\Queue\ShouldQueue;
use Illuminate\Mail\Mailable;
use Illuminate\Queue\SerializesModels;

class Message extends Mailable
{
    use Queueable, SerializesModels;

    public $mailData;

    /**
     * Create a new message instance.
     *
     * @return void
     */
    public function __construct($mailData)
    {
        $this->mailData = $mailData;
    }

    /**
     * Build the message.
     *
     * @return $this
     */
    public function build()
    {
        //return $this->markdown('emails.message');
      return $this->from('sender@email.com','Sender Name')->replyTo('sender@email.com')
        ->subject('Contact Message')
        ->view('emails.message');
    }
}
````

## Create controller

````shell
php artisan make:controller MessageController --resource --model=Message
````

> Controller :  /app/Http/Controllers/ContactController.php

````php
<?php

namespace App\Http\Controllers;

use App\Models\Message;
use Illuminate\Http\Request;
use Illuminate\Support\Facades\Mail;

class MessageController extends Controller
{
  /**
   * Display a listing of the resource.
   *
   * @return \Illuminate\Http\Response
   */
  public function index()
  {
    return view('forms.contact');
  }

  /**
   * Show the form for creating a new resource.
   *
   * @return \Illuminate\Http\Response
   */
  public function create()
  {
    //
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
      'body' => 'required',
    ]);
  
    Mail::to('reciever@email.com')
      ->send(new \App\Mail\Message($request->all()));

    return redirect()->route('messages.index')->with('ok','sent !');
  }

  /**
   * Display the specified resource.
   *
   * @param  \App\Models\Message $message
   * @return \Illuminate\Http\Response
   */
  public function show(Message $message)
  {
    //
  }

  /**
   * Show the form for editing the specified resource.
   *
   * @param  \App\Models\Message $message
   * @return \Illuminate\Http\Response
   */
  public function edit(Message $message)
  {
    //
  }

  /**
   * Update the specified resource in storage.
   *
   * @param  \Illuminate\Http\Request $request
   * @param  \App\Models\Message $message
   * @return \Illuminate\Http\Response
   */
  public function update(Request $request, Message $message)
  {
    //
  }

  /**
   * Remove the specified resource from storage.
   *
   * @param  \App\Models\Message $message
   * @return \Illuminate\Http\Response
   */
  public function destroy(Message $message)
  {
    //
  }
}
````

## Create views

1.  `/resources/views/forms/contact.blade.php`

> Contact Form

````php
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport"
        content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Laravel Basic Mail</title>
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/css/bootstrap.min.css" rel="stylesheet"
        integrity="sha384-KyZXEAg3QhqLMpG8r+8fhAXLRk2vvoC2f3B09zVXn8CA5QIVfZOJ3BCsw2P0p/We" crossorigin="anonymous">
</head>
<body>
<div class="container">
  <div class="row">
    <div class="col-12">
      <h1 class="display-4">Send New Message</h1>
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

  @if ($message = Session::get('ok'))
    <div class="alert alert-success">
      <p>{{ $message }}</p>
    </div>
  @endif

  <div class="row">
    <div class="col">
      <form action="{{route('messages.store')}}" method="post">
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
          <label for="body" class="form-label">Message</label>
          <textarea name="body" type="tel" class="form-control form-control-sm" rows="4" required></textarea>
        </div>
        <div class="mb-3">
          <button type="submit" class="btn btn-sm btn-primary">send</button>
        </div>
      </form>
    </div>
  </div>
</div>
<script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.0/dist/js/bootstrap.bundle.min.js"
        integrity="sha384-U1DAWAznBHeqEIlVSCgzq+c9gqGAJn5c/t99JyeKa9xxaYpSvHU5awsuZVVFIhvj"
        crossorigin="anonymous"></script>
</body>
</html>
````

2. `/resources/views/emails/message.blade.php`

> Mail Body

````php
<!doctype html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport"
        content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Message</title>
</head>
<body>
<ul>
  <li><b>Name:</b> {{$mailData['name']}}</li>
  <li><b>Email:</b> {{$mailData['email']}}</li>
  <li><b>Message:</b> {{$mailData['body']}}</li>
</ul>
</body>
</html>
````


## Create routes

> /routes/web.php

````php
use App\Http\Controllers\MessageController;
// {***} ///
Route::resource('messages', MessageController::class);
````

## Serve

````shell
php artisan serve
````

> navigate to : http://127.0.0.1:8000/messages
