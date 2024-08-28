#linux #flatpak #vscode
# Instalação e configuração inicial

```shell
flatpak install com.visualstudio.code
```

O pacote flatpak do Visual Studio Code exige algumas configurações extras para funcionar corretamente dentro do ambiente Sandbox. A integração do terminal com o sistema operacional exige está configuração:
```json
"terminal.integrated.defaultProfile.linux": "bash",
"terminal.integrated.profiles.linux": {
	"bash": {
		"path": "host-spawn",
		"args": [
			"bash"
		]
	}
}
```

> [!tip] Outros tipos de shell
> Você pode optar por utilizar o zsh, fish, etc... o importante é manter o comando `host-spawn` para permitir a integração com o host (S.O.)

# SDKs
#php
O VSCode possui algumas extensões que necessitam de executáveis instalados na máquina, porém como o flatpak isola tudo em Sandbox, é necessário instalar esses executáveis/bibliotecas via _runtimes_ do flatpak, por exemplo no caso do PHP:

```
flatpak install org.freedesktop.Sdk.Extension.php83
```

> [!WARNING] Versão do SDK/runtime
> Certifique-se que o runtime que será instalado está na mesma versão de SDK que o pacote do VSCode, no exemplo acima apenas a versão 8.3 do PHP está disponível para o SDK 23.08 que é o utilizado pelo VSCode. Versões diferentes não são compatíveis e não serão listadas no ambiente compartilhado do Sandbox.
> 
> Você pode conferir a versão do SDK de um pacote com o comando:
> `flatpak info --show-sdk <APP_ID>`

## Ativando/utilizando o SDK
Basta iniciar a aplicação com a variável de ambiente `FLATPAK_ENABLE_SDK_EXT` desta forma:

```shell
FLATPAK_ENABLE_SDK_EXT=php83 flatpak run com.visualstudio.code
```

> [!TIP] Habilitando ENV com Flatseal
> É possível utilizar a aplicação "Flatseal" para inserir essa ENV de forma permanente, permitindo lançar a aplicação pela interface gráfica da distribuição já com a injeção desta.

Nas configurações do VSCode é necessário inserir as linhas abaixo:

```json
{
	"php.executablePath": "/usr/lib/sdk/php83/bin/php",
	"php.validate.executablePath": "/usr/lib/sdk/php83/bin/php",
	//--- Se estiver usando essa extensão
	"LaravelExtraIntellisense.phpCommand": "/usr/lib/sdk/php83/bin/php -r \"{code}\"",
}
```

## Login e sincronização
O sistema de sincronização do VSCode exige que o login seja feito por uma conta Github ou Microsoft, e uma vez que o login seja feito para persistir a sessão é necessário que o VSCode tenha acesso ao gerenciador de chaves do sistema operacional.
### Gnome Keyring
#gnome 
Para garantir o funcionamento do VSCode Flatpak com o Gnome Keyring é necessário editar o arquivo `~/.vscode/argv.json` adicionando a seguinte linha:

```json
"password-store": "gnome-libsecret"
```

### KWallet
#kde
Para garantir o funcionamento do VSCode Flatpak com o KWallet é necessário editar o arquivo `~/.vscode/argv.json` adicionando a seguinte linha:
```json
"password-store": "kwallet5"
```

Além disso é necessário adicionar permissões no flatpak do VSCode para acesso ao DBus do KDE `--talk-with=org.kde.\*`, que pode ser realizado através do gerenciador de permissões nativo do KDE ou Flatseal, na seção "Session Bus".
![[vscode_kde_flatpak_session_bus_permission.png]]

