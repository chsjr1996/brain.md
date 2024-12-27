Similar ao método `lazy`, o `cursor` pode ser utilizado para reduzir significantemente a memória consumida pela aplicação quando se está iterando por miliares de *models* Eloquent.

Contudo, isso não significa que serão realizadas múltiplas consultas no banco de dados, apenas uma é executa mas a "hidratação" dos *models* Eloquent  será realizada individualmente para cada iteração. Dessa forma apenas um *model* Eloquent será mantido na memória por vez.

> [!warning] Atenção
> O método `cursor` não é compatível com o recurso `eager load`. Portanto, se for necessário utilizar este recurso, considere usar o método `lazy`.

# Exemplos
Iterando com `foreach`:
```php
use App\Models\Flight;

foreach (Flight::where('destination', 'Zurich')->cursor() as $flight) {

// ...

}
```

O método `cursor` retorna uma "LazyCollection" que por sua vez disponibiliza diversos métodos já também disponíveis em uma "Collection" típica do Laravel.
```php
use App\Models\User;

$users = User::cursor()->filter(function (User $user) {

return $user->id > 500;

});

foreach ($users as $user) {

echo $user->id;

}
```

---

> [!NOTE] Referências
> - [Laravel Docs - Eloquent Cursors](https://laravel.com/docs/11.x/eloquent#cursors)
