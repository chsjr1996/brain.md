# Instalação do projeto

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


# Executando servidor reverb
```sh
php artisan reverb:start
```

> [!QUOTE] Mudando host e porta
> Por padrão o reverb executa no endereço e porta `0.0.0.0:8080`, mas é possível passar os parâmetros `--host=127.0.0.1` e `--port=9000` para mudar.

# Preparando arquivos
Criando Model `ChatMessage`
```sh
php artisan make:model ChatMessage --migration
```

---

## Referências
- [Laravel News - Real time chat](https://laravel-news.com/laravel-real-time-chat)
- [Laravel Docs - Reverb](https://laravel.com/docs/12.x/reverb#introduction)
- [Laravel Docs - Broadcasting](https://laravel.com/docs/12.x/broadcasting#client-side-installation)