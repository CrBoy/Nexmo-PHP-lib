Sending SMS via the Nexmo SMS gateway.
======================================

Installation
------------

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
[user@project_path]\$ composer require crboy/nexmo-php-lib
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Quick Examples
--------------

1.  Sending an SMS

    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    $sms = new NexmoMessage(‘account_key’, ‘account_secret’);
    $sms->sentText(‘+886912345678’, ‘MyApp’, ‘Hello, World!’);
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

2.  Recieving SMS

    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    $sms = new NexmoMessage('account_key', 'account_secret');
    if ($sms->inboundText()) {
        $sms->reply('You said: ' . $sms->text);
    }
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

3.  Recieving a message receipt

    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    $receipt = new NexmoReceipt();
    if ($receipt->exists()) {
        switch ($receipt->status) {
            case $receipt::STATUS_DELIVERED:
                // The message was delivered to the handset!
                break;
            case $receipt::STATUS_FAILED:
            case $receipt::STATUS_EXPIRED:
                // The message failed to be delivered
                break;
        }
    }
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

4.  List purchased numbers on your account

    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    $account = new NexmoAccount('account_key', 'account_secret');
    $numbers = $account->numbersList();
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Most Frequent Issues
--------------------

### Sending a message returns false.

This is usually due to your webserver unable to send a request to Nexmo. Make
sure the following are met:

1.  Either CURL is enabled for your PHP installation or the PHP option 'allow_url_fopen' is set to 1 (default).

2.  You have no firewalls blocking access to rest.nexmo.com/sms/json on port 443.

### Your message appears to have been sent but you do not recieve it.

Run the example.php file included. This will show any errors that are returned
from Nexmo.
