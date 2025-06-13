Pest é um *framework* de testes que foca na simplicidade, sua base é construída em cima do PHPUnit, ou seja, trata-se de uma abstração para facilitar a implementação desta suite de testes, baseando-se em uma sintaxe similar ao Jest (na qual foi inspirado).

## Instalação
Instale o Pest como uma dependência de desenvolvimento. O comando irá remover o PHPUnit como dependência direta, mas ele será instalado como dependência do Pest.

> [!warning] Atenção
> O Pest requer PHP 8.2 ou superior.

```sh
composer remove phpunit/phpunit
composer require pestphp/pest --dev --with-all-dependencies
```

Em seguida inicialize o Pest no projeto com o seguinte comando:

```sh
./vendor/bin/pest --init
```

---
## Exemplos
- [[Pest - Laravel TestCase e migrations]]
- [[Pest - verificando array de objetos]]

---
## Referências
- [Pest site](https://pestphp.com/)