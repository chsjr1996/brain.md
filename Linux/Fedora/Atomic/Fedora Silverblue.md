#linux #fedora #atomic 

Fedora Silverblue é um [[Sistemas imutáveis]] que dispõe por padrão o ambiente gráfico Gnome.

## Utilidades
- [[Primeiros passos pós instalação]]
- [[Brain.md/Dev/Containers/Podman/Podman problemas de permissões]]
- [[Toolbox ajustes e correções]]


### docker-compose
Download and install from docker-compose Github repository, it should work with `podman compose` : )

### Install and use without reboot
Install using `rpm-ostree install` and after it run this command:

```
sudo rpm-ostree apply-live
```
