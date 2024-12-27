#linux #hardware #udev
## Bloquear teclado interno do notebook
Adicione um novo arquivo no diretório `/etc/udev/rules.d` chamado (por exemplo) `99-disable_laptop_keyboard.rules`. Neste arquivo adicione o identificador do teclado, neste caso `AT Translated Set 2 keyboard`.

```
KERNEL=="event*", ATTRS{name}=="AT Translated Set 2 keyboard", ENV{LIBINPUT_IGNORE_DEVICE}="1"
```

> [!warning] Atenção
> No Fedora Atomic deixe um deploy fixado antes dessa modificação caso seja necessário revertê-la. E caso esteja utilizando Sway, opte por usar o bloqueio direto nos arquivos de configuração do compositor.

### Bloqueio via compositor Sway
#sway
Adicione o seguinte trecho no arquivo de configuração do Sway:

```
input "1:1:AT_Translated_Set_2_keyboard" events disabled
```
