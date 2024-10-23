Caso o site apresente algum erro de redirecionamento, e/ou acuse algum problema de *cookies* pode ser que seja necessário forçar o SSL no Admin (e site). Para isto, basta editar o arquivo `wp-config.php` inserindo o trecho abaixo:

```php
/* Add any custom values between this line and the "stop editing" line. */

define( 'FORCE_SSL_ADMIN', true );

if (strpos($_SERVER['HTTP_X_FORWARDED_PROTO'], 'https') !== false) {
   $_SERVER['HTTPS']='on';
}
```
