Com Inertia é possível criar uma aplicação "monolítica moderna", onde o *backend* e *frontend* ainda estão em uma 'estrutura de projeto' única, porém se comportando como duas aplicações API e SPA.

Dessa forma o *frontend* pode ser escrito com React, VueJS ou Svelte e integrado com *frameworks backend* como Laravel ou Ruby on Rails de forma que toda navegação se comporte como uma SPA.

Isso possibilita escrever um código mais organizado e otimizado, se beneficiando de todas as funcionalidades dos *frameworks backend* mas ainda mantendo um *frontend* moderno.

> [!quote] Observações
> O Inertia não é um *framework* e nem mesmo uma implementação *server-side* ou *client-side*, mas sim projetado para integrar *backend* e *frontend* em uma estrutura moderna. "Pense no Inertia como uma cola entre essas partes", essa biblioteca possui adaptadores para interligá-las.

# Instalação server-side
É possível utilizar o *framework backend*  Laravel ou Ruby on Rails, porém neste arquivo está contemplada apenas a instalação e configuração do Laravel.

Primeiro instale a biblioteca em seu projeto pelo `composer`:
```sh
composer require inertiajs/inertia-laravel
```

Modifique o template principal (geralmente `app.blade.php`) para conter este código inicial:
```php blade
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0" />
    @vite('resources/js/app.js')
    @inertiaHead
  </head>
  <body>
    @inertia
  </body>
</html>
```
> É possível mudar o template principal usando o método `Inertia::setRootView()`.

Agora instale o *middleware* pelo `artisan`:
```sh
php artisan inertia:middleware
```

E adicione este *middleware* no grupo 'web' no arquivo `bootstrap/app.php`:
```php
use App\Http\Middleware\HandleInertiaRequests;
//...
->withMiddleware(function (Middleware $middleware) {
    $middleware->web(append: [
        HandleInertiaRequests::class,
    ]);
})
```
> Isso considerando o Laravel 11+, até o 10 isso deve ser feito no arquivo `app/Http/Kernel.php`.

Agora basta criar uma rota que aponte para um método em algum *controller* que retorne a resposta do tipo "Inertia":
```php
use Inertia\Inertia;

class EventsController extends Controller
{
    public function show(Event $event)
    {
        return Inertia::render('Event/Show', [
            'event' => $event->only(
                'id',
                'title',
                'start_date',
                'description'
            ),
        ]);
    }
}
```
> O arquivo "Show.jsx" (ou "Show.vue") precisa existir no diretório `resources/views/Pages/Event`

# Instalação client-side
É possível instalar a biblioteca para *client-side* para integrar com VueJS, React ou Svelte. Considere a instalação utilizando o Vite como ferramenta de build, mas dependendo da versão do Laravel é  possível que ainda esteja utilizando o Laravel Mix.

## React
Considerando que seja React, prossiga com a instalação da seguinte forma:
```sh
npm install @inertiajs/react
```

Crie um arquivo chamado `app.js` dentro de `resources/js` contendo:
```js
import { createInertiaApp } from '@inertiajs/react'
import { createRoot } from 'react-dom/client'

createInertiaApp({
  resolve: name => {
    const pages = import.meta.glob('./Pages/**/*.jsx', { eager: true })
    return pages[`./Pages/${name}.jsx`]
  },
  setup({ el, App, props }) {
    createRoot(el).render(<App {...props} />)
  },
})
```
> Para Webpack/Laravel Mix consultar o site.


---
> [!NOTE] Referências
> - [Inertia site](https://inertiajs.com/)
