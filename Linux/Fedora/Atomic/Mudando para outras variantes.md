	#linux #fedora #atomic 

Uma das características de sistemas imutáveis do Fedora, é a capacidade de mudar de "variante", ou seja, trocar o ambiente da distribuição para outra imagem na árvore do `ostree`, este processo pode ser feito através da rotina de 'rebase'.

Segue um exemplo de como mudar do `Silverblue` (variante com Gnome) para o `Kinoite` (variante com KDE Plasma).

## "Backup"
Primeiro fixe a versão atual do deu "deploy" que se encontra na posição zero.
```
sudo ostree admin pin 0
```
> Isso garante que um backup caso algo dê errado, já que os "deploys" não são todos mantidos dependo da quantidade de alteração realizadas.

> [!NOTE] Observação
> Os deploys são contados iniciando de zero, ou seja, o primeiro e atual deploy não é o número "um", mas sim o número "zero".

## Preparando para o 'rebase'
Primeiro, pesquise pelas opções disponíveis do "fedora".
```
ostree remote refs fedora
```
> Você pode utilizar o pipe + grep para filtrar no final deste comando, ex: ` | grep -i kinoite`.

Depois de localizar a variante desejada, basta realizar o "rebase":
```
rpm-ostree rebase fedora:fedora/40/x86_64/kinoite
```

> [!important] Atenção
> Cuidado com a versão do Fedora e a arquitetura quando escolher a variante, você deve manter a mesma arquitetura do seu processador e evitar mudar para versões ainda não lançadas do Fedora.

## Antes de reiniciar - Cuidados adicionais
### Desfazer fstab/rbind
No caso de ter feito o procedimento do [[SDDM - Fedora Kinoite|SDDM]] é necessário comentar/remover o `rbind`, e após a reinicialização, se necessário deletar o diretório `/var/sddm`.

### Reiniciar dconf/gsettings
Esse procedimento pode ser útil para limpar configurações aplicadas em outra DE, seja a transição do Silverblue (Gnome) para Kinoite (KDE) ou vice-versa.

```sh
gsettings reset-recursively org.gnome.desktop.interface
```

```sh
gsettings reset-recursively org.gnome.desktop.wm.preferences
```

### Configurações da variante atual
Essa etapa pode ser útil para salvar as configurações aplicadas pela variante atual, e usadas para comparação e alterações na nova variante se necessário.
```sh
sudo ostree admin config-diff > variant_settings.txt
```

## Reiniciando - Aplicando alteração
Agora basta reiniciar sua máquina que no próximo boot o novo "deploy" será selecionado automaticamente, e você já estará na variante que foi feito o "rebase".

---
## Desfazendo o 'rebase'
Para desfazer isso, reinicie sua máquina e aperte "shift" antes da tela de boot do Fedora, e então selecione o "deploy" da variante anterior. Após o boot, no terminal execute o comando abaixo:

```
rpm-ostree rollback
```
 > Esse comando fará com que o "deploy" atual selecionado antes do boot, seja o primeiro "deploy" da lista nos próximos boots, ou seja, o "deploy" padrão.
 

Se necessário, você pode executar o comando para remover um "deploy" fixado
```
sudo ostree admin pin --unpin 2
```
> Remove o "deploy" de número dois.

---

> [!NOTE] Referências
> - [Possible to install Kinoite over Silberblue while keeping HOME?](https://discussion.fedoraproject.org/t/possible-to-install-kinoite-over-silberblue-while-keeping-home/82449/6)
> - [Rebasing Kinoite (Fedora 38) to Silverblue (Fedora 38) Issues](https://www.reddit.com/r/Fedora/comments/165szab/rebasing_kinoite_fedora_38_to_silverblue_fedora/)
> - 
