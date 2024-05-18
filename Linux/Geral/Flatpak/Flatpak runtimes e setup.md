Em determinados casos é necessário instalar _runtimes_ no flatpak, que variam desde utilitários à bibliotecas que poderão ser compartilhadas entre as aplicações flatpak via Sandbox.

# Instalando _runtimes_

Você pode procurar por SDKs desta forma:

```shell
flatpak search org.freedesktop.Sdk.Extension | grep -i <term>
```

E então instalar com:

```shell
flatpat install org.freedesktop.Sdk.Extension.php83
```

## Encontrando os arquivos dos _ runtimes_

Pelo repositório do flathub no Github é possível verificar o "path" de onde será instalado a biblioteca/executável do _runtime_.

...

Você também pode acessar uma aplicação desejada e verificar se a biblioteca/executável está presente no diretório `/usr/bin` ou `/usr/lib/sdk`. Por exemplo o VSCode:

```shell
flatpak run --command=sh com.visualstudio.code
ls /usr/bin
ls /usr/lib/sdk
```


---

## Aplicações
[[Flatpak - VSCode]]