Para trocar o wallpaper do SDDM no Fedora Kinoite é necessário criar um diretório paralelo e vincular este com o diretório do SDDM. Para isso execute os passos abaixo:

1. Copie o diretório `/usr/share/sddm` para dentro de `/var`
```
sudo cp -r /usr/share/sddm /var
```

2. Modifique o arquivo `/etc/fstab` adicionando o diretório `/var/sddm`
```
/var/sddm /usr/share/sddm none rbind 0 0
```

> [!NOTE] Referência
> [Reddit r/Fedora - Kinoite: How can I change login background?](https://www.reddit.com/r/Fedora/comments/12ywfst/comment/jhqk4th/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)
