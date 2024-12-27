#revisar #melhorar

O Laravel Socialite possibilita a integração com provedores OAuth de autenticadores como:
- Facebook
- X (Twitter)
- Linkedin
- Google
- Github
- GitLab
- Bitbucket
- Slack

As plataformas listadas acima são atualmente suportadas pela biblioteca, porém é possível utilizar adaptadores feitos pela comunidade para extender essa lista. Veja mais no site [Socialite Providers](https://socialiteproviders.com/).

O Socialite permite a integração de forma simplificada através de Facades, por exemplo, integrar-se com o login do Github exige apenas a configuração das credencias e um pequeno trecho de código:

## Exemplo de configuração Github
```php
'github' => [
    'client_id' => env('GITHUB_CLIENT_ID'),
    'client_secret' => env('GITHUB_CLIENT_SECRET'),
    'redirect' => 'http://example.com/callback-url',
],
```
>`config/services.php`

> [!quote] Observações
> Essas credenciais podem ser criadas/obtidas através de sua conta Github, esse processo é similar para as outras plataformas.


## Exemplo de implementação com Github
```php
use Laravel\Socialite\Facades\Socialite;
 
Route::get('/auth/redirect', function () {
    return Socialite::driver('github')->redirect();
});
 
Route::get('/auth/callback', function () {
    $user = Socialite::driver('github')->user();
 
    // $user->token
	// $user->name
	// etc...
});
```

Todo fluxo é gerido internamente pela Facade, e se o login for bem sucedido a variável `$user` receberá o objeto contendo informações do usuário como "name", "email", entre outros, de forma que será possível utilizar esses dados internamente em sua aplicação.

---
## Referências
- [Laravel Doc - Socialite](https://laravel.com/docs/11.x/socialite)