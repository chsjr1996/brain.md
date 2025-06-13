# Laravel scratch tinker
```php
<?php

//region boot
require 'vendor/autoload.php';
$app = require_once '/var/www/bootstrap/app.php';

$kernel = $app->make(Illuminate\Contracts\Console\Kernel::class);
$kernel->bootstrap();
//endregion
```

# Encrypt and decrypt com helper Str
```php
<?php
//...
$encryptedToken = str('token-ultra-secret')
	->encrypt()
	->prepend('encrypted')
	->append(':end');
```

# Condicionais com when
```php
<?php
//...
when(app()->isLocal(), function () {
	Route::get('/test', [ControllerTest::class, 'show'])/
});
```
> pode ser util para declarar rotas para testar e-mails, ativar fluxos ou rotinas manualmente, etc...