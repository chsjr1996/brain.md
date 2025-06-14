# Instalação inicial do projeto

Criando a aplicação Laravel:
```sh
laravel new laravel-reverb-chat-lab
```
> **Neste "cenário"** é usado o instalador para garantir a inicialização do kit Inertia.JS + Vue

Instalação de libs
```sh
php artisan install:broadcasting
```
> Server side

```sh
npm install --save-dev laravel-echo pusher-js
```
> Para instalar libs Client side (projetos já existentes)

> [!WARNING] Atenção
> O comando `install:broadcasting` em projetos **inicializados com kits** já deve injetar o código necessário no arquivo `resources/js/app.ts` para injetar o 'echo' na aplicação.
> 
> Segundo a documentação é necessário modificar o arquivo `resources/js/bootstrap.js` mas este não existe e não é necessário neste cenário.

# Preparando arquivos
Criando Model `ChatMessage`
```sh
php artisan make:model ChatMessage --migration
```

Configurando variáveis de ambiente caso não tenham sido definidas ainda
```
BROADCAST_CONNECTION=reverb
REVERB_APP_ID=1234  
REVERB_APP_KEY=the-secret-key  
REVERB_APP_SECRET=the-secret-secret  
REVERB_HOST=0.0.0.0  
REVERB_PORT=8080  
REVERB_SCHEME=http  
  
VITE_REVERB_APP_ID="${REVERB_APP_ID}"  
VITE_REVERB_APP_KEY="${REVERB_APP_KEY}"  
VITE_REVERB_APP_SECRET="${REVERB_APP_SECRET}"  
VITE_REVERB_HOST="${REVERB_HOST}"  
VITE_REVERB_PORT="${REVERB_PORT}"  
VITE_REVERB_SCHEME="${REVERB_SCHEME}"
```

# Executando servidor reverb
```sh
php artisan reverb:start
```

> [!QUOTE] Mudando host e porta
> Por padrão o reverb executa no endereço e porta `0.0.0.0:8080`, mas é possível passar os parâmetros `--host=127.0.0.1` e `--port=9000` para mudar.

# FAQ

## Erro ao conectar com reverb
Certifique-se de que configurou as variáveis de ambiente corretamente. Caso não esteja usando o modo server do vite, faça build novamente da aplicação. Além disso tente limpar o cache de configurações do Laravel:
```sh
php artisan optimize:clear
```

Pode ser que o navegador tenha guardado cache também, então após limpar usando o comando acima, no navegador use o 'force refresh' CTRL+SHIFT+F (ou CTRL+SHIFT+F5).

---

## Referências
- [Laravel News - Real time chat](https://laravel-news.com/laravel-real-time-chat)
- [Laravel Docs - Reverb](https://laravel.com/docs/12.x/reverb#introduction)
- [Laravel Docs - Broadcasting](https://laravel.com/docs/12.x/broadcasting#client-side-installation)
- [Medium - Real-Time chat @emreensr](https://medium.com/@emreensr/real-time-chat-implementation-with-laravel-reverb-and-vue-3-03a16cf593ef)
- [LogRocket - realt-time chat @rosariodechiara](https://blog.logrocket.com/building-real-time-chat-app-using-laravel-reverb-vue/)