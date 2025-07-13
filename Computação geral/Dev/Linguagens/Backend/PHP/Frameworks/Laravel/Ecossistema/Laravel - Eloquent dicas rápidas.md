### Relations default value
Caso a relação não exista é possível usar um valor padrão definido direto no Model.
```php
// Post model
public function user(): BelongsTo
{
    return $this->belongsTo(
        User::class
    )->withDefault([
        'name' => 'Guest Author'
    ]);
}
```

```php
// before
$post->user?->name ?? 'Guest Author';

// after
$post->user->name;
```

### Atualizando campo de data
Ao invés de atribuir `now()` à coluna e depois salvar a entidade no BD, é possível usar o método `touch()`, ex:
```php
// ao invés de
$user->verified_at = now();
$user->save();

// usar
$user->touch('verified_at');
```

---
## Referências
- [Laravel - Eloquent Relationships](https://laravel.com/docs/12.x/eloquent-relationships)