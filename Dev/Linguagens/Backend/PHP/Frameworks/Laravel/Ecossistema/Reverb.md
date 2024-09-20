#laravel #websocket

Com está biblioteca é possível criar aplicações "*real time*" por comunicação com *WebSocket* extremamente rápidas e escaláveis, integrando-se com a aplicação Laravel e toda suíte disponível de [*broadcast* de eventos](https://laravel.com/docs/11.x/broadcasting).

# Instalação e configuração
Instale o `reverb` utilizando o `artisan`:
```sh
php artisan install:broadcasting
```
> Este é um comando interativo, opte por instalar o `reverb` durante as etapas e compilar o frontend também.

Define as variáveis de ambiente:
```
REVERB_APP_ID=my-app-id
REVERB_APP_KEY=my-app-key
REVERB_APP_SECRET=my-app-secret
```

## Vite
Para o Vite é necessário adicionar as variáveis de ambiente com o prefixo "VITE_", portanto, defina as variáveis desta forma:
```
VITE_REVERB_HOST="localhost"
VITE_REVERB_PORT="8080"
VITE_REVERB_APP_ID="${REVERB_APP_ID}"
VITE_REVERB_APP_KEY="${REVERB_APP_KEY}"
VITE_REVERB_APP_SECRET="${REVERB_APP_SECRET}"
```

## Laravel Sail
Expondo os arquivos do Laravel Sail:
```sh
sail artisan sail:publish
```

Modificando o arquivo do `supervisor` em `docker/8.3/supervisord.conf`:
```
[supervisord]
//...
minfds=10000

//...
[program:reverb]
command=php /var/www/html/artisan reverb:start --host="0.0.0.0" --port=8080 --hostname="laravel.test"
autostart=true
autorestart=true
user=%(ENV_SUPERVISOR_PHP_USER)s
redirect_stderr=true
stdout_logfile=/var/www/html/storage/logs/reverb.log
```

> [!quote] Observações
> A configuração `mindfds=10000` permite ao `reverb` abrir mais conexões através do `supervisor` para possibilitar um maior número de clientes conectados simultâneamente.


---

> [!NOTE] Referências
> - [Laravel Docs - Reverb](https://laravel.com/docs/11.x/reverb)
> - [Medium - How to use Reverb with Laravel Sail
](https://medium.com/@martio-appcadabra/how-to-use-reverb-with-laravel-sail-aa7c8450a76c)
