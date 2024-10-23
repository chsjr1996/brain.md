#brainstart #os #linux

# Distros
## Rolling release
- [[ArchLinux]]

## Atomic/imutável
- [[Fedora Atomic - Definição|Fedora Atomic]]

## Hardware
- [[Ajustes no hardware]]
- [[Linux hardware - dicas e utilidades]]
- [[Linux - Drivers de vídeo]]

## Aplicativos e utilitários

> [!NOTE] Mudando aplicativo padrão via CMD
> É possível mudar o aplicativo padrão por tipo de arquivo via linha de comando, [[Aplicativos padrão|leia mais aqui]].

- [[Flatpak]]
- [[Snap]]
- [[Steam]]

---
# Containers
Veja mais na seção dedicada [[Containers|containers]].

# Interfaces gráficas

### X11
O "X window system" ou X11 é um servidor gráfico utilizado por longos anos para disponibilizar aplicações gráficas no Linux.

### Protocolo Wayland
Diferente do X11 o Wayland não é um servidor gráfico, mas sim um protocolo que especifica a comunicação entre clientes e o hardware, pelo qual pode ser utilizado para criar os [[Compositor gráfico|compositores gráficos]].

### Gerenciadores de janela
Em distribuições Linux, um gerenciador de janelas é responsável por organizar as janelas determinando o posicionamento e dimensões. Existem tipos de gerenciadores de janelas distintos, mas a maioria são baseados no conceito "Stack", como os que são utilizados nos ambientes gráficos [[Gnome]] e [[KDE]] por exemplo.

Também existem os gerenciadores conhecidos como "tiling window manager" que permitem organizar as janelas em um outro modelo, focado em dividir a geometria das janelas por quadrantes seja de forma manual ou automática. São utilizados em interfaces gráficas como [[Sway]] e [[i3wm]] por exemplo.

Além disso também existem os "compositores de janelas", estes permitem a adição de efeitos nas janelas como sombra, transparência, blur, entre outros. Os compositores wayland também exercem a função de gerenciadores de janela.

**TWM (X11/Wayland)**
- [[i3wm]] (X11)
- [[Sway]] (Wayland)

## Ambientes gráficos
- [[Gnome]]
- [[KDE]]

---
# Dicas e utilidades
- [[Linux - Comandos utilitários]]

---
## Referências
- [X Window System](https://en.wikipedia.org/wiki/X_Window_System)