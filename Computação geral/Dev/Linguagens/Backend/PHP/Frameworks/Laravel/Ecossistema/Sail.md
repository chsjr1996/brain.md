#laravel #podman #docker

Essa biblioteca permite a instalação de uma interface de comandos de linha para interagir com a ambientação do Docker (via container*) para desenvolvimento de aplicações com Laravel.

> [!quote] Observação
> A ambientação não se limita apenas do Docker, é possível utilizar o Podman também.

Ao invés de construir toda ambientação do zero, com essa biblioteca é possível escolher alguns componentes para serem adicionados no arquivo `docker-compose.yml` que são mais comuns em projetos com *framework* Laravel. Desta forma, instalar essa biblioteca permite a criação de um ambiente de desenvolvimento de maneira simplificada, mas poderosa.

# Instalação
Primeiro adicione a biblioteca com `composer`:
```sh
composer require laravel/sail --dev
```

Agora instale os arquivos necessários com `artisan`:
```sh
php artisan sail:install
```

> [!quote] Observação
> Esse etapa é interativa, aqui você pode escolher quais containers deseja utilizar além do padrão para executar a aplicação em si. Por exemplo, você pode adicionar containers para banco de dados, simulação de caixa de entrada de e-mails, etc...

# Executando comandos
Uma vez que os arquivos foram instalados, é possível iniciar a aplicação desta forma:
```sh
./vendor/bin/sail up
```

> [!tip] Dica
> Para facilitar o uso, é possível criar o atalho (alias) no arquivo `.bashrc` (ou `.zshrc`) apontando para o diretório do sail desta forma:
> ```sh
> alias sail='sh $([ -f sail ] && echo sail || echo vendor/bin/sail)'
> ```
> 
> Então estando no diretório da aplicação Laravel, o comando acima ficaria assim:
> ```sh
> sail up
> ```

Outros exemplos de comandos:
- `sail up -d` (inicia a aplicação e libera o terminal)
- `sail down` (para e remove os containers)
- `sail stop` (apenas para os containers)
- `sail artisan` (executa comandos artisan dentro do container)
- `sail php` (executa comandos PHP dentro do container)
- `sail composer` (executa comandos composer dentro do container)
- `sail node` (executa comandos node dentro do container)
- `sail npm` (executa comandos npm dentro do container)
- `sail yarn` (executa comandos yarn dentro do container)
- `sail tinker` (atalho para artisan tinker)
- `sail shell` (executa o bash dentro do container)
- `sail root-shell` (executa o bash como root dentro do container)
- `sail share` (compartilha a aplicação de forma publica)

# Configuração
Atenção ao arquivo `.env`, os apontamentos devem usar os nomes de serviço estabelecidos pelo `docker-compose.yml` assim como numa aplicação com a ambientação construída do zero.

# Xdebug
O Xdebug é incluso no Laravel Sail, para ativá-lo basta usar a variável de ambiente abaixo antes de iniciar os containers:
```sh
SAIL_XDEBUG_MODE=develop,debug,coverage
```
> Exemplo: `SAIL_XDEBUG_MODE=develop,debug,coverage sail up`

---

> [!NOTE] Referências
> - [Laravel Docs - Sail](https://laravel.com/docs/11.x/sail)
