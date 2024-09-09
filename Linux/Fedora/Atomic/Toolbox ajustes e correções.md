#linux #fedora #atomic 
## xdg-open
Para permitir abrir o aplicativo correspondendo na máquina "host" de links e/ou arquivos quando aplicações que estejam executando dentro do `toolbox` solicitem sua abertura, é necessário realizar um ajuste no utilitário `xdg-open`. Para isso, rode os comandos abaixo no terminal:

```
toolbox enter
```
> Para entrar no toolbox.

```
sudo dnf install flatpak-xdg-utils
```
> Instala o pacote `flatpak-xdg-utils`.

```
sudo mv /usr/bin/xdg-open /usr/bin/xdg-open_old
```
> "Remove" o binário original.

```
sudo ln -s /usr/bin/flatpak-xdg-open /usr/bin/xdg-open
```
> Associa o `flatpak-xdg-open` com `xdg-open` com uso de link simbólico.

Para testar, dentro do `toolbox` execute:
```
xdg-open https://github.com
```
>  Deve abrir o navegador padrão definido na máquina host.
