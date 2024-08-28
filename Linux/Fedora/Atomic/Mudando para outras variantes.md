	#linux #fedora #atomic 

Uma das características de sistemas imutáveis do Fedora, é a capacidade de mudar de "variante", ou seja, trocar o ambiente da distribuição para outra imagem na árvore do `ostree`.

Segue um exemplo de como mudar do `Silverblue` (variante com Gnome) para o `Kinoite` (variante com KDE Plasma).

Primeiro fixe a versão atual do deu "deploy" que se encontra na posição zero.
```
sudo ostree admin pin 0
```
> Isso garante que um backup caso algo dê errado, já que os "deploys" não são todos mantidos dependo da quantidade de alteração realizadas.

> [!NOTE] Observação
> Os deploys são contados iniciando de zero, ou seja, o primeiro e atual deploy não é o número "um", mas sim o número "zero".


Pesquise pelas opções disponíveis do "fedora".
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

Agora basta reiniciar sua máquina que no próximo boot o novo "deploy" será selecionado automaticamente, e você já estará na variante que foi feito o "rebase".

---
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