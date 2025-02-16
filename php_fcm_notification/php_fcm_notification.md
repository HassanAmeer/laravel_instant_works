# PHP FCM Notification new v1 Legacy (2025)

- folder structure like this
- -- vendor/
- -- send.php
- -- fcm_configration.json

  
### 1. install google auth

 - for mac
```php
  sudo composer require google/auth
```


### 2. 
```php
require_once('vendor/autoload.php');

use Google\Auth\Credentials\ServiceAccountCredentials;
use Google\Auth\HttpHandler\HttpHandlerFactory;

if(isset($_POST['btnClicked'])){
    $credentials = new ServiceAccountCredentials(
        'https://www.googleapis.com/auth/firebase.messaging',
        json_decode(file_get_contents('fcm.json'), true)
    );
    $token = $credentials->fetchAuthToken(HttpHandlerFactory::build());
    
    $accessToken = $token['access_token']; // generate server token valid for 1 hour by default
    
    $ch = curl_init("https://fcm.googleapis.com/v1/projects/wodl-50f48/messages:send");
    
    curl_setopt($ch, CURLOPT_HTTPHEADER, [
        'Content-Type: application/json',
        'Authorization: Bearer ' . $accessToken
    ]);
    
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_VERBOSE, true);
    
    $notification = [
        'message' => [
             // fcm token
            'token' => 'ex5mXjoiSuSvX2XWtAea6E:APA91bHmIF217sRuMuupv_GTpnQX-pPKYEIT_EG13ekzfIQHjm6fwLPTcKs3dhNeEVhzb2y-6diVKzHmw5hXXUz-M1rR1YC_fBfolO6TXNt4a6N6Mn9qkww',
            'notification' => [
                'title' => 'Hello',
                'body' => 'World',
                'image' => 'https://www.google.com/images/branding/googlelogo/2x/googlelogo_color_120x44dp.png'
            ],
             // optional
            "webpush": {
                "fcm_options": {
                    "link": "https://google.com"
                }
            },
            'android' => [
                'priority' => 'high',
                'ttl' => '3600s',
            ],
            'data' => [
                'mydata' => json_encode(['messagefrom' => 'server01', 'type' => 'test'])
            ]
        ]
    ];
    
    curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($notification));
    
    $response = curl_exec($ch);
    
    if (curl_errno($ch)) {
        echo 'fcm Curl error: ' . curl_error($ch);
    } else {
        echo "fcm response:".$response;
    }
    
    curl_close($ch);
    
    echo '<pre>';
    print_r("response: " . $response);
    print_r("token: " . $token);
    echo '</pre>';
}


```
