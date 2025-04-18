

## Error on bind port 80
Caso apresente esse erro é necessário informar ao sistema que porta 80 pode ser liberada para uso por aplicações sem privilégio de super usuário.

```sh
sudo sysctl net.ipv4.ip_unprivileged_port_start=80
```

Para persistir essa mudança, adicione a linha abaixo no arquivo `/etc/sysctl.d/99-sysctl.conf`.

```sh
net.ipv4.ip_unprivileged_port_start=80
```

> [!warning] Atenção
> Veja a seção "Permissões adicionais" abaixo.

## Permission Denied

> [!warning] Atenção
> Veja a seção "Permissões adicionais" abaixo. Com a instrução de `user: root` não se faz necessário usar o `unshare`. Lembre-se que isso só deve ser feito para containers 'seguros'/confiáveis, pois permite o acesso total do container aos volumes compartilhados.

Com o Podman é comum acontecer alguns erros de permissão em determinados diretórios, como por exemplo o diretório "storage", ou então o arquivo do PHPUnit. Uma possível solução pode ser alcançada através do comando `podman unshare`.

```
podman unshare ls -al <app_container_directory_path>
```
> Isso vai exibir com qual usuário os diretórios estão associados dentro do podman, e consequentemente com qual usuário eles serão associados dentro do container em execução.


Defina o grupo com o UID e logo após dê permissão total para o dono+grupo (rwx-rwx-rx)
```
podman unshare chown -R :1000 <app_container_directory_path>
```

```
podman unshare chmod -R 775 <app_container_directory_path>
```

> [!quote] Observação
> O UID utilizado no exemplo é `1000`, mas deve ser alterado para o UID atual, para visualizar basta entrar com o comando `echo $UID`. Esse comando fará com que o usuário associado com o container seja o mesmo que o usuário local, e pode ser usado em casos onde o container não precisa de permissões elevadas para executar.

---

## Permissões adicionais
Ainda pode ser necessário adicionar algumas instruções no `docker-compose.override.yml` para habilitar o acesso à porta 80 e escrita nos diretórios:

```yml
	service_name:
      cap_add:
        - NET_BIND_SERVICE
      user: root
```

### Referências
- [Using volumes with rootless podman, explained](https://www.tutorialworks.com/podman-rootless-volumes/)
- [Container permission denied: How to diagnose this error](https://www.redhat.com/sysadmin/container-permission-denied-errors)
