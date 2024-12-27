# AMD
Primeiramente verifique qual driver está em uso pelo comando no terminal:
```sh
lspci -k | grep -EA3 'VGA|3D|Display'
```

Se constar `amdgpu` o driver correto/apropriado já está em uso. Caso contrário será necessário instalar o driver e Vulkan juntamente, como neste comando por exemplo:
```sh
sudo dnf install xorg-x11-drv-amdgpu mesa-vulkan-drivers.x86_64 mesa-vulkan-drivers.i686 vulkan-loader.x86_64 vulkan-loader.i686 vulkan-tools
```

Modifique o grud `/etc/default/grub` adicionando no final da variável `GRUB_CMDLINE_LINUX`:
```
amdgpu.si_support=1
```
>Para GPUs "*Southern Island*".

```
amdgpu.cik_support=1
```
> Para GPUs "*Sea Island*"

| GPU família     | Modelos                                                | Parâmetro            |
| --------------- | ------------------------------------------------------ | -------------------- |
| Southern Island | HD7750-HD7970, R9 270, R9 280, R9 370X, R7 240, R7 250 | amdgpu.si_support=1  |
| Sea Island      | HD7790, R7 260, R9 290, R7 360, R9 390                 | amdgpu.cik_support=1 |
Aplique as mudanças no grupo com:
```sh
 sudo grub2-mkconfig -o /boot/efi/EFI/fedora/grub.cfg
```
> Para sistemas com EFI

```sh
sudo grub2-mkconfig -o /boot/grub2/grub.cfg
```
> Para sistemas BIOS (sem EFI)

Reinicie o sistema.

# Obtendo informações
Para verificar informações sobre GPU, APIs gráficas (OpenGL, Vulkan), entre outros, no terminal os seguintes comandos:

| Comando                                    | Descrição                                                                |
| ------------------------------------------ | ------------------------------------------------------------------------ |
| `glxinfo -B`                               | Obtem informações básicas sobre a GPU (Fabricante, modelo, VRAM, etc...) |
| `vulkaninfo --sumary`                      | Obtém informações sobre a API gráfica Vulkan                             |
| `lspci -k \| grep -EA3 'VGA\|3D\|Display'` | Obtém informações de hardware e drivers em uso                           |

---

> [!NOTE] Referências
> - [The Specter - amgpu](https://thespecter.net/blog/technology/enabling-amdgpu-on-fedora-31-for-using-vulkan-with-r7-and-r9-radeon-cards/)
 
