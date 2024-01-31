
//-------------------------------------------------------------------------//
//-------------------------------------------------------------------------//
//-------------------------------------------------------------------------//
//------------------- Laravel 10 send Email With Smtp ---------------------//
//-------------------------------------------------------------------------//
//-------------------------------------------------------------------------//
// 1. run this command =>  php artisan make:mail emailClassName
// -> its generate a class on this path -> app/Mail/emailClassName.php

// 2. then set configration
//  -> path: config/mail.php
// in mail.php add configration like =>
//  'smtp' => [
//             'transport' => 'smtp',
//             'url' => env('MAIL_URL'),
//             'host' => env('MAIL_HOST', 'smtp.mailgun.org'),
//             'port' => env('MAIL_PORT', 587),
//             'encryption' => env('MAIL_ENCRYPTION', 'tls'),
//             'username' => env('MAIL_USERNAME'),
//             'password' => env('MAIL_PASSWORD'),
//             'timeout' => null,
//             'local_domain' => env('MAIL_EHLO_DOMAIN'),
//         ], // optional for write same.
//  -> after this in .env file set email smtp configration with original information

// 3. make or add templateName.blade.php in html code in resources/view folder -> for get value use {{$getvaluebythisname}} from app/Mail/emailClassName.php file from build function return view(templateName) if pass a value then attach -> with(getvaluebythisname=>value)
// a. constructor function for get value where this class is called
// protected $name;
// public function __construct($getName)
// {
//     $this->name = $getName;
// }
// b. set template name in content function. i think its optional.
// public function content(): Content
// {
//     return new Content(
//         view: 'templateFolderName.templateName',
//     );
// }
// c. in build function add tempate thats want to show in email
// public function build() {
//     return $this->view("templateFolderName.templateName")
//     ->replyTo("email@gmail.com","Wiz-Stamp") // if add to reply
//     ->with(array("getvaluebythisname"=>$this->name)); // if pass a values like in array
// }
// 4. for send email call emailClassName thats you make by commands from controllers function etc
// $check = Mail::to($emailis)->send(new emailClassName($resetCode));
// and import this Mail,and emailClassName where form
// like this:|
// use Illuminate\Support\Facades\Mail;
// use App\Mail\emailClassName;
