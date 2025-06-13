
# Autenticação
Por padrão só é possível acessar o Telescope em ambientes locais, ou seja, que possuem a variável de ambiente `APP_ENV` definida para `local`.

Para garantir que o acesso será permitido em produção basta alterar o código do método `gate` em `app/Providers/TelescopeServiceProvider.php` para filtrar quem pode ou não ter acesso, por exemplo:
```php
use App\Models\User;
 
/**
 * Register the Telescope gate.
 *
 * This gate determines who can access Telescope in non-local environments.
 */
protected function gate(): void
{
    Gate::define('viewTelescope', function (User $user) {
        return in_array($user->email, [
            'taylor@laravel.com',
        ]);
        // or if 'user' has some field to check his role.
        // return $user->is_admin;
    });
}
```