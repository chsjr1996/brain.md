#linux

Para verificar o aplicativo padrão por "mime type" execute o comando:

```
xdg-mime query default inode/directory
```
> Isso vai exibir qual aplicação é responsável por abrir esse tipo "mime"

Para trocar a aplicação padrão, execute:

```
xdg-mime default <app> inode/directory
```
> Substituir `<app>` pela aplicação deseja, exemplo: `thunar.desktop`