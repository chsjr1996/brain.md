#podman

É possível utilizar o Docker Compose com Podman, basta apenas baixar o binário no repositório e colocá-lo no diretório correto, conforme os passos a seguir:

Acessar a página de lançamento e baixar o último executável:

```
https://github.com/docker/compose/releases
```
---
```shell
wget https://github.com/docker/compose/releases/download/v2.28.1/docker-compose-linux-x86_64
```
>Exemplo  usando a versão `v2.28.1`.
---

```shell
mkdir -p ~/.docker/cli-plugins
```
>Use este comando caso o diretório acima não exista.

```shell
mv docker-compose-linux-x86_64 ~/.docker/cli-plugins/docker-compose
```
>É necessário que o binário seja movido para esse diretório com o nome `docker-compose`.

Após isso já deve ser possível utilizar o comando `podman compose` que irá utilizar o binário acima para gerenciar containers.
