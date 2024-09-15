Essa biblioteca permite a instalação de uma dashboard para monitoramento de filas gerenciadas pelo [[Redis Queues]].

O Horizon permite monitorar filas utilizando chaves que variam desde *tags* até classes, nome das filas, etc... a fim de coletar e disponibilizar métricas para acompanhamento de tudo o que é processado em *background* pela aplicação.

# Instalação
Primeiro instale a biblioteca pelo `composer`:
```sh
composer require laravel/horizon
```

Após isso instale os arquivos necessários pelo `artisan`:
```sh
php artisan horizon:install
```

# Autenticação
A dashboard do Horizon é disponibilizada por pela rota `/horizon`. Por padrão, está rota permite o acesso apenas em ambientes locais (`APP_ENV=local`). Porém, é possível habilitar o acesso para ambientes de produção, para isso basta configurar o arquivo `app/Providers/HorizonServiceProvider.php` definindo um "*gate*" de autorização desta forma, por exemplo:
```php
/**
 * Register the Horizon gate.
 *
 * This gate determines who can access Horizon in non-local environments.
 */
protected function gate(): void
{
    Gate::define('viewHorizon', function (User $user) {
        return in_array($user->email, [
            'taylor@laravel.com',
        ]);
        // or if 'user' has some field to check his role.
        // return $user->is_admin;
    });
}
```

> [!quote] Observação
> A lógica de autenticação dentro do "Gate" pode ser implementada de acordo com suas necessidades, basta retornar "true" ou "false" para garantir ou bloquear o acesso.

---
> [!NOTE] Referências
> - [Laravel Docs - Horizon](https://laravel.com/docs/11.x/horizon)
