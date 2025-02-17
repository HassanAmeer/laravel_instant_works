



```php

<?php $path= dirname(__FILE__,4);
require_once $path.'/smtp/vendor/autoload.php';
use PHPMailer\PHPMailer\PHPMailer;
use PHPMailer\PHPMailer\SMTP;
use PHPMailer\PHPMailer\Exception;
use PHPMailer\PHPMailer\OAuth;
use League\OAuth2\Client\Provider\Google;




// function phpsmtpmailer($to, $subject, $body) 
// { 
	 // $refreshToken='1//04b9IxHIG9U6sCgYIARAAGAQSNwF-L9IrqomKfJNiTxQSg652DfhgV9tKjO_kW1BhRObJkkkxd9Zf7DXQQY6QhqfHHooMYIhQSqc';
     $mail = new PHPMailer();
        $mail->isSMTP();
        $mail->SMTPAuth = true;

		$mail->Host = 'smtp.gmail.com';
		$mail->Port = 465; // For SSL
		$mail->SMTPSecure = PHPMailer::ENCRYPTION_SMTPS; // Use PHPMailer::ENCRYPTION_STARTTLS for port 587

        // $mail->AuthType = 'XOAUTH2';
		$mail->Username = 'support@wodl.app';
		$mail->Password = 'jptbggzzeteuikvw';

//         $provider = new Google(
//             [
//                                'abc-testabceutheo.apps.googleusercontent.com',
//                 'clientId' => 'testabc',
//                 'clientSecret' => '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',
//             ]
//         );

//         $mail->setOAuth(
//             new OAuth(
//                 [
//                     'provider' => $provider,
//                     'clientId' => 'abc-abceutheo.apps.googleusercontent.com',
//                     'clientSecret' => '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',
//                     'refreshToken' => $refreshToken,
//                     'userName' => 'support@wodl.app',
//                 ]
//             )
//         );
		
		$mail->setFrom('support@wodl.app', 'WODL');

//receiver email address and name
$mail->addAddress('hasanameer386@gmail.com'); 
$mail->isHTML(true);
 
$mail->Subject = 'test';
// $mail->Subject = $subject;
// $mail->Body    = $body;
$mail->Body    = 'mail test';

// Attempt to send the email
if (!$mail->send()) {
    echo 'Email not sent. An error was encountered: ' . $mail->ErrorInfo;
} else {
    echo 'Message has been sent.';
}

$mail->smtpClose();
// }



```
