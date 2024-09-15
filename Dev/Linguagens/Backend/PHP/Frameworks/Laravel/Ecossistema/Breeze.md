#laravel-starter-kit

Esta biblioteca é um kit que permite a instalação de diversas funcionalidades relacionadas ao fluxo de autenticação do Laravel, como login, cadastro, recuperação de senha, verificação de e-mail e confirmação de senha. Além disso também trás uma versão simplificada da tela 'Meu perfil', onde o usuário logado pode alterar seu nome, e-mail e senha.

Por padrão, as *views* disponibilizadas são no formato Blade e estilizadas com Tailwind CSS. Porém, é possível optar pelos formatos Livewire ou Inertia - Laravel, neste último caso podendo seguir com VueJS ou React.

# Instalação
Primeiro é necessário adicionar a biblioteca no projeto usando o `composer`:
```sh
composer require laravel/breeze --dev
```

Logo após a instalação da biblioteca, é necessário instalar os arquivos desse kit usando o `artisan`:
```sh
php artisan breeze:install
```

> [!quote] Observações
> A instalação é feita de forma interativa, onde é possível escolher entre Blade, Livewire ou Inertia.

Após isso é necessário executar as `migrations` para instalação/configuração da base de dados com as tabelas necessárias:
```sh
php artisan migrate
```

Dependendo da escolha, é necessário também executar o processo de build/dev pelo `vite`, onde é necessário instalar as dependências primeiramente:
```sh
npm install
```

```sh
npm run dev
```
>Ou `npm run build`

---

> [!NOTE] Referências
> - [Laravel - Starter kits Breeze](https://laravel.com/docs/11.x/starter-kits#laravel-breeze)
