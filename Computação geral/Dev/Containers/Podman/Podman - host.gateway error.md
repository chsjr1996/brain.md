O Podman não é compatível por padrão com a configuração `host.docker.internal:host-gateway` utilizada em algumas aplicações. Portanto, executar o `podman compose` em algum arquivo que contenha essa instrução irá ocasionar um erro, e existem duas formas de contornar isso.

# Alterando configurações
Para permitir usar essa instrução basta criar/modificar o arquivo `~/.config/containers/containers.conf` adicionando o seguinte trecho:
```
[network]
default_rootless_network_cmd = "slirp4netns"
```

# Alterando docker-compose
Caso não queira alterar a configuração padrão como citado acima, então crie um arquivo no mesmo diretório onde encontra-se o `docker-compose.yml`  chamado `docker-compose.override.yml`, contendo:
```
services:
    laravel.test:
        extra_hosts: !reset []
        volumes:
            - '.:/var/www/html:z'
        environment:
            XDEBUG_CONFIG: '${SAIL_XDEBUG_CONFIG:-client_host=10.0.0.137}'
```
