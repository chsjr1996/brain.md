```php
expect($response->getStatusCode())->toBe(Response::HTTP_OK)  
    ->and($response->json('data'))->each()->toHaveKeys([  
        'id',  
        'name',  
        'email',  
    ]);
```
