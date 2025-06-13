Essa funcionalidade adiciona a sintaxe do PHP a possibilidade de definir as lógicas de `get` e `set` diretamente as propriedades de classe, sem ter a necessidade de criar estes métodos separadamente.

```php
<?php

declare(strict_types=1);
 
class User
{
    public string $fullName {
        // Dynamically build up the full name from
        // the first and last name
        get => $this->firstName.' '.$this->lastName;
 
        // Split the full name into first and last name and
        // then set them on their respective properties
        set(string $name) {
            $splitName = explode(' ', $name);
            $this->firstName = $splitName[0];
            $this->lastName = $splitName[1];
        }
    }
 
    public string $firstName {
        set(string $name) => $this->firstName = ucfirst($name);
    }
 
    public string $lastName {
        set(string $name) => $this->lastName = ucfirst($name);
    }
 
    public function __construct(string $fullName) {
        $this->fullName = $fullName;
    }
}
 
$user = new User(fullName: 'foo bar');
 
echo $user->firstName; // Foo
echo $user->lastName; // Bar
echo $user->fullName; // Foo Bar
```

---

> [!NOTE] Referências
> - [Ash Allen Design - PHP 8.4 Property Hooks](https://ashallendesign.co.uk/blog/php-84-property-hooks)
> - [PHP - RFC Property Hooks](https://wiki.php.net/rfc/property-hooks)
