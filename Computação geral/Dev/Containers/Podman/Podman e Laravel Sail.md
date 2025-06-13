#podman 

Por padrão o Laravel Sail funciona apenas com Docker, porém é possível utilizá-lo com Podman. Para isso basta seguir os passos abaixo.

## Modificando .env
Primeiro é necessário modificar o `.env` da aplicação inserindo estes valores:

```
WWWGROUP=1000
WWWUSER=1000
SAIL_SKIP_CHECKS=true
```
> `SAIL_SKIP_CHECKS` é necessário para evitar que o Sail verifique se o Docker está executando, que nesse caso retornaria erro sempre que o comando `sail` fosse utilizado.

## Arquivo de socket
Também é necessário indicar o arquivo de socket utilizado pelo Podman para permitir se comunicar com esta ferramenta, isso pode ser feito através da variável de ambiente `DOCKER_HOST`, por exemplo:

 ```
 export DOCKER_HOST='unix:///run/user/1000/podman/podman.sock'
 ```
 > Normalmente o caminho onde se encontra o `podman.sock` é este, porém dependendo da configuração da distro, ele pode estar em outro diretório.

---

> [!quote] Observação
> Caso apresente o erro acusando não ter encontrado o comando `docker-compose`, basta criar o link simbólico da seguinte forma:
> ```sh
> ln -s /home/user/.docker/cli-plugins/docker-compose /home/user/.local/bin
> ```


