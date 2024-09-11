## Corrigindo problema DBus activatable
Ao tentar abrir o aplicativo via interface gráfica ([[Gnome]] ou [[KDE]]) é possível que ela não inicialize corretamente.  Para resolver siga os passos abaixo:


1. Localize o arquivo `.desktop` do flatpak, normalmente está neste diretório:
```sh
/var/lib/flatpak/exports/share/applications/
```

2. Copie o arquivo `org.gnome.Hamster.desktop` para:
```sh
/home/<USER>/.local/share/applications/org.gnome.Hamster.GUI.desktop
```


> [!NOTE] Observação
> Observe que o nome do arquivo foi modificado para ter `GUI` para que desta forma o acesso ao DBus seja garantido corretamente.


---

> [!NOTE] Referência
> https://github.com/flathub/org.gnome.Hamster/issues/2#issuecomment-1586017434
