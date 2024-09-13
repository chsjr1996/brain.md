Essa biblioteca disponibiliza recursos para automação de navegação pela aplicação, criando um navegador de internet capaz de executar ações via script de forma expressiva e de fácil uso.

Por padrão implementa um driver individual do [Chrome](https://sites.google.com/chromium.org/driver), porém é possível instalar outro compatível com [[Selenium]] se necessário.

# Instalação
Adicione a biblioteca no projeto usando o `composer`:
```sh
composer require laravel/dusk --dev
```

Instale os arquivos necessários com `artisan`:
```sh
php artisan dusk:install
```

# Gerenciando drivers
É possível mudara a versão do driver Chrome pelo `artisan`, seguem alguns exemplos:
```sh
# Install the latest version of ChromeDriver for your OS...

php artisan dusk:chrome-driver

# Install a given version of ChromeDriver for your OS...

php artisan dusk:chrome-driver 86

# Install a given version of ChromeDriver for all supported OSs...

php artisan dusk:chrome-driver --all

# Install the version of ChromeDriver that matches the detected version of Chrome / Chromium for your OS...

php artisan dusk:chrome-driver --detect
```

# Criando testes
Crie o arquivo com `artisan`, por exemplo:
```sh
php artisan dusk:make LoginTest
```

É possível utilizar o [[PHPUnit]] diretamente ou o [[Pest]], segue abaixo os exemplos de cada um:

**PHPUnit**
```php
<?php
 
namespace Tests\Browser;
 
use App\Models\User;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Laravel\Dusk\Browser;
use Tests\DuskTestCase;
 
class ExampleTest extends DuskTestCase
{
    use DatabaseMigrations;
 
    /**
     * A basic browser test example.
     */
    public function test_basic_example(): void
    {
        $user = User::factory()->create([
            'email' => 'taylor@laravel.com',
        ]);
 
        $this->browse(function (Browser $browser) use ($user) {
            $browser->visit('/login')
                    ->type('email', $user->email)
                    ->type('password', 'password')
                    ->press('Login')
                    ->assertPathIs('/home');
        });
    }
}
```

**Pest**
```php
<?php
 
use App\Models\User;
use Illuminate\Foundation\Testing\DatabaseMigrations;
use Laravel\Dusk\Browser;
 
uses(DatabaseMigrations::class);
 
test('basic example', function () {
    $user = User::factory()->create([
        'email' => 'taylor@laravel.com',
    ]);
 
    $this->browse(function (Browser $browser) use ($user) {
        $browser->visit('/login')
                ->type('email', $user->email)
                ->type('password', 'password')
                ->press('Login')
                ->assertPathIs('/home');
    });
});
//
```

---

> [!NOTE] Referências
> - [Laravel Docs - Dusk](https://laravel.com/docs/11.x/dusk)
