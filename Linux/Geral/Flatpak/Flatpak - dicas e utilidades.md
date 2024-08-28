#flatpak 

## Chromium apps Wayland
#gnome #kde

Caso as aplicações criadas como atalhos do Chromium/Chrome no flatpak não estiverem sendo associadas com o ícone na Dash do Gnome ou outro painel, faça as seguintes modificações no arquivo ".desktop".

```shell
cd ~/.local/share/applications
```

Identifique o arquivo `.desktop` que corresponde a aplicação através do "Name" no arquivo, e altere a linha que contem "StartupWMClass" trocando o prefixo de `crx_` para `chrome-` e acrescentando no final o ID do perfil. Desta forma esse atributo "StartupWMClass" ficará igual ao "Icon", por exemplo:

**Antes**
```
Icon=chrome-hnpfjngllnobngcgfapefoaidbinmjnm-Default
StartupWMClass=crx_hnpfjngllnobngcgfapefoaidbinmjnm
```

**Depois**
```
Icon=chrome-hnpfjngllnobngcgfapefoaidbinmjnm-Default
StartupWMClass=chrome-hnpfjngllnobngcgfapefoaidbinmjnm-Default
```

## KDE Breeze
#kde 

```
sudo flatpak override --system --filesystem=xdg-config/gtk-3.0:ro --filesystem=xdg-config/gtkrc-2.0:ro --filesystem=xdg-config/gtk-4.0:ro --filesystem=xdg-config/gtkrc:ro
```
> Referência: [Github -  flathub/org.gtk.Gtk3theme.Breeze](https://github.com/flathub/org.gtk.Gtk3theme.Breeze/blob/master/README.md)