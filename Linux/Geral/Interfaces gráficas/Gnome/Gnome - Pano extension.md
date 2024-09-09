#gnome 

A extensão "Pano - Clipboard Manager" ainda não foi aprovada no Gnome Extensions, e portanto, é necessário instalar manualmente.
> [!NOTE] Gnome 46
> Isso afeta apenas a compatibilidade com Gnome 46 até o dia 28/06/2024. É possível que este problema seja resolvido a qualquer momento e essa ação não seja mais necessária.

## Etapas para compilação e instalação
Primeiro clone o repositório, depois faça o build usando `yarn` e crie um link simbólico da extensão, da seguinte forma:
```shell
git clone https://github.com/oae/gnome-shell-pano.git
```

```shell
cd ./gnome-shell-pano
```

```shell
yarn install
```

```shell
yarn build
```

```shell
ln -s "$PWD/dist" "$HOME/.local/share/gnome-shell/extensions/pano@elhan.io"
```
