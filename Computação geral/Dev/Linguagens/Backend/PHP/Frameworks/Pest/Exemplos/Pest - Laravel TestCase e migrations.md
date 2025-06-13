Isso garante a inicialização dos serviços internos do Laravel, permitindo o uso de recursos do *framework*. Também garante a execução das *migrations* entre os testes, reiniciando a base de dados a cada teste executado.

```php
pest()->extend(TestCase::class)
	->use(RefreshDatabase::class);
``` 