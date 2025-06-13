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

---
## Referências
- [Laravel - Eloquent Relationships](https://laravel.com/docs/12.x/eloquent-relationships)