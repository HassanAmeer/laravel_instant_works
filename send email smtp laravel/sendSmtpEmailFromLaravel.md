
//-------------------------------------------------------------------------//
//-------------------------------------------------------------------------//
//-------------------------------------------------------------------------//
//------------------- Laravel 10 send Email With Smtp ---------------------//
//-------------------------------------------------------------------------//
//-------------------------------------------------------------------------//

# Laravel 10 - Sending Email with SMTP

1. **Generate Email Class:**
   - Run the following command to create a new mail class:
     ```bash
     php artisan make:mail EmailClassName
     ```
   - The class EmailClassName will be generated at `app/Mail/EmailClassName.php`.

2. **SMTP Configuration:**
   - Open `config/mail.php` and configure SMTP settings: can write same
     ```php
     'smtp' => [
         'transport' => 'smtp',
         'host' => env('MAIL_HOST', 'smtp.mailgun.org'),
         'port' => env('MAIL_PORT', 587),
         'encryption' => env('MAIL_ENCRYPTION', 'tls'),
         'username' => env('MAIL_USERNAME'),
         'password' => env('MAIL_PASSWORD'),
         'timeout' => null,
         'local_domain' => env('MAIL_EHLO_DOMAIN'),
     ],
     ```
   - also Set SMTP configuration in the `.env` file but .env is with original information

3. **Create Email Template:**
   - Add or create an email template (e.g., `TemplateName.blade.php`) in the `resources/views` folder.
   - Use `{{$getvaluebythisname}}` in template and for display values passed from the mail class -> EmailClassName if Need.
     
4. **Mail Class Setup:**
   - Open the generated mail class (`app/Mail/EmailClassName.php`).
   - Define any variables in the constructor that you want to pass to the email template like this.
     ```php
       protected $variableName;
       public function __construct($getValue)
       {
           $this->variableName = $getValue;
       }

     ```
   - Set the template name in the `content` method.
   - In the `build` method, specify the template and any additional options thats you needs:
     ```php
     public function build()
     {
         return $this->view('templateFolderName.templateName')
             ->replyTo('name@gmail.com', 'Main Title') // Optional: Add a reply-to address
             ->with(['getvaluebythisname' => $this->variableName]); // Optional: Pass values to the template
     }
     ```

5. **Sending Email:**
   - Call the mail class in your controllers or other functions:
     ```php
     use Illuminate\Support\Facades\Mail;
     use App\Mail\EmailClassName;
     
     $check = Mail::to($to@gmail.com)->send(new EmailClassName($sendValue));
     ```
   - Make sure to import the necessary classes.


*. **Clear Cache and Troubleshooting:**
   - In case of any issues related to SMTP or sending emails, run the following commands to clear cache and restart necessary services:
     - Clear configuration cache:
       ```bash
       php artisan config:cache
       ```
     - Clear configuration files:
       ```bash
       php artisan config:clear
       ```
     - Clear application cache:
       ```bash
       php artisan cache:clear
       ```
     - Restart the queue worker (if applicable):
       ```bash
       php artisan queue restart
       ```

   - Alternatively, you can create a custom route for clearing cache and other related tasks:
     - Add the following route in your `web.php` or `routes/web.php` file:
       ```php
       Route::get('/clear/cache', function () {
           $run = Artisan::call('config:clear');
           $run = Artisan::call('cache:clear');
           $run = Artisan::call('config:cache');
           $run = Artisan::call('route:clear');
           // $run = Artisan::call('view:clear');
           return 'Cache Cleared';
       });
       ```
     - Access this route in your browser or through a tool like Postman to clear the cache manually.


6. **Additional Notes:**
   - Customize the template and class according to your requirements.
   - Ensure that the email template is well-designed and contains dynamic content using Blade syntax.

7. **Troubleshooting:**
   - Check the Laravel documentation for any additional troubleshooting steps.
   - Verify that your SMTP server details are correct.

Feel free to customize and expand upon these points based on your project's specific needs.


------------------------------------------- other way ------------------------------------------------------------

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
//     ->replyTo("email@gmail.com","Main Title") // if add to reply
//     ->with(array("getvaluebythisname"=>$this->name)); // if pass a values like in array
// }
// 4. for send email call emailClassName thats you make by commands from controllers function etc
// $check = Mail::to($emailis)->send(new emailClassName($resetCode));
// and import this Mail,and emailClassName where form
// like this:|
// use Illuminate\Support\Facades\Mail;
// use App\Mail\emailClassName;


