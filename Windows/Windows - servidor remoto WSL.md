Para trabalhar a partir de uma outra máquina utilizando o Windows como servidor web e ainda ter a possibilidade de editar os arquivos via SSH são necessários alguns ajustes.

## Acessar servidor web WSL externamente
Para tornar possível acessar o servidor web criado dentro do WSL é necessário editar o arquivo `.wslconfig` presente no diretório do usuário e acrescentar o seguinte trecho:

```ini
[wsl2]
;...
networkingMode=mirrored
```

Agora a partir de um terminal **admin** verifique se as regras de firewall para WSL2 estão disponíveis:

```sh
Get-NetFirewallHyperVVMCreator
```
> Caso não retorne nada, significa que a versão instalada do WSL2 não é suportada para esse procedimento, sendo necessário atualizar para versão `2.0.9.0` ou superior.

Ainda no terminal **admin** execute:

```sh
New-NetFirewallHyperVRule `
-DisplayName 'Allow All Inbound Traffic to WSL in Private Network' `
-Name 'WSL Private Inbound Rule' `
-Profiles Private `
-Direction Inbound `
-Action Allow `
-VMCreatorId ((Get-NetFirewallHyperVVMCreator).VMCreatorId) `
-Enabled True
```
> Essa é a forma mais segura, porém só permite o acesso ao WSL em redes privadas.


> [!quote] Observações
> Para desfazer essa regra, execute:
> ``` sh
> Remove-NetFirewallHyperVRule -Name 'WSL Private Inbound Rule'
> ```

**Atenção** essa forma desativa o firewall para WSL2 completamente, apenas use se for acessar de forma externa à rede privada.
```
Set-NetFirewallHyperVVMSetting -Name ((Get-NetFirewallHyperVVMCreator).VMCreatorId) -Enabled False
```

Reinicie o WSL:
```sh
wsl --shutdown
```

```
wsl
```

E execute algum servidor web para testar, por exemplo:
```sh
python3 -m http.server
```

## SSH no WSL
Utilizar o SSH diretamente no WSL possibilita acessar o Linux dentro da máquina virtual "diretamente" sem passar pelo terminal do Windows, e dessa forma também facilitando a configuração do "remote code" do VSCode.

Primeiro, instale o `openssh-server` no Ubuntu (WSL):
```sh
sudo apt install openssh-server
```

Caso a instalação apresente algum erro, edite o arquivo de socket do SSH para mudar a porta, pois deve ser um conflito com a porta 22, também utilizada pelo Remote SSH do WIndows:
```sh
sudo systemctl edit ssh.socket
```

No arquivo, na parte superior conforme instruído pelos comentários, adicione:
```ini
[Socket]
ListenStream=
ListenStream=2222
```

> [!warning] Atenção
> É importante manter as duas linhas com `ListenStream`, caso contrário o SSH tentara utilizar a porta 22 e 2222 ao mesmo tempo.

Reinstale o SSH:
```sh
sudo apt remove openssh-server && sudo apt install openssh-server
```

E se necessário reinicie:
```sh
sudo systemctl restart ssh
```

Verifique se a porta configurada está sendo utilizada, onde a porta 22 não deve aparecer:
```sh
sudo lsof -i -P -n | grep LISTEN
```

## SSH no Windows
Acesse as configurações do sistema `WIN+I` e vá em `Sistema > Recursos opcionais` (final da página) e acesse "Exibir recursos" e procure por "OpenSSH" marque para instalar a prossiga.

Ao finalizar confira o diretório `C:\Windows\System32\OpenSSH\` no explorer, onde deve estar localizado os arquivos do OpenSSH (sshd, ssh-agent, etc...).

Agora configure o SSH, primeiro verificando os serviços:
```sh
Get-Service -Name *ssh*
```
> Deve retornar o status dos serviços que devem estar parados por padrão.

Inicie os serviços, e também defina para inicializarem automaticamente no boot (opcional).
```sh
Start-Service sshd
```

```sh
Set-Service -Name sshd -StartupType 'Automatic'
```
> Opcional

```sh
Start-Service 'ssh-agent'
```

```sh
Set-Service -Name 'ssh-agent' -StartupType 'Automatic'
```
> Opcional

Habilite o acesso a porta 22 via regra de firewall (requer terminal com privilégio **admin**):
```sh
netsh advfirewall firewall add rule name=”SSHD service” dir=in action=allow protocol=TCP localport=22
```

Para acessar o "PowerShell" ao invés do CMD quando acessar o SSH, execute no terminal **admin**:
```sh
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## Windows Remote Desktop 
Acesse as configurações do Windows `WIN+I` e vá em `Sistema > Área de Trabalho Remota` e ative a opção.

### login com senha RDP
Também será necessário se logar no Windows pelo menos uma vez utilizando a senha da conta caso tenha sido configurado para entrar com Windows Hello (PIN ou FaceID, etc...).

Para isso, nas configurações vá em `Contas > Opções de entrada` e desative a opção "Para aumentar a segurança, permitir apenas a entrada do Windows Hello para contas Microsoft neste dispositivo". Efetue o logout e na tela de entrada troque de PIN (ou FaceID) para senha e efetua o login com senha.

Feito isso basta se logar em um RDP client usando o mesmo usuário e senha, mesmo que o usuário seja um endereço de e-mail, a senha neste caso será a mesma utilizada para entrar na conta Microsoft. Em tese isso é necessário apenas uma vez, e a partir disso você já reativar a opção acima.

---
## Referências
- [Access a web server which is running on WSL (Windows Subsystem for Linux) from the local network - Stack Overflow](https://stackoverflow.com/questions/49835559/access-a-web-server-which-is-running-on-wsl-windows-subsystem-for-linux-from-t)
- [How to SSH into Windows 10 or 11?](https://gist.github.com/teocci/5a96568ab9bf93a592d7a1a237ebb6ea)
- [How to change the SSH server port on Ubuntu? - Server Fault](https://serverfault.com/questions/1159599/how-to-change-the-ssh-server-port-on-ubuntu)
- [visual studio code - VSCode: how to ssh remote connect to remote WSL2 - Stack Overflow](https://stackoverflow.com/questions/63563693/vscode-how-to-ssh-remote-connect-to-remote-wsl2)