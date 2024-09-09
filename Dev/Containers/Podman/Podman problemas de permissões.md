		#podman 


## Error on bind port 80
Caso apresente esse erro é necessário informar ao sistema que porta 80 pode ser liberada para uso por aplicações sem privilégio de super usuário.

```
sudo sysctl net.ipv4.ip_unprivileged_port_start=80
```

Para persistir essa mudança, adicione a linha abaixo no arquivo `/etc/sysctl.d/99-sysctl.conf`.

```
net.ipv4.ip_unprivileged_port_start=80
```

## Permission Denied
Com o Podman é comum acontecer alguns erros de permissão em determinados diretórios, como por exemplo o diretório "storage", ou então o arquivo do PHPUnit. Uma possível solução pode ser alcançada através do comando `podman unshare`.

```
podman unshare ls -al <app_container_directory_path>
```
> Isso vai exibir com qual usuário os diretórios estão associados dentro do podman, e consequentemente com qual usuário eles serão associados dentro do container em execução.


```
podman unshare chown 1000:1000 -R <app_container_directory_path>
```
> O UID utilizado no exemplo é `1000`, mas deve ser alterado para o UID atual, para visualizar basta entrar com o comando `echo $UID`. Esse comando fará com que o usuário associado com o container seja o mesmo que o usuário local, e pode ser usado em casos onde o container não precisa de permissões elevadas para executar.

### Referências
- [Using volumes with rootless podman, explained](https://www.tutorialworks.com/podman-rootless-volumes/)
- [Container permission denied: How to diagnose this error](https://www.redhat.com/sysadmin/container-permission-denied-errors)
