#linux #fedora #atomic 

## Ajustando o uso de SWAP
O uso do SWAP é definido pela distribuição Linux onde em alguns casos este valor pode estar ajustado em 60%, ou seja, quando 40% da memória RAM estiver ocupada o sistema operacional irá instruir o uso da SWAP.

Isso pode não ser o ideal principalmente para hardwares com SSD e com uma quantidade de memória RAM superior à 16GB, pois não há necessidade do uso precoce de SWAP nesse caso. Além disso, o uso excessivo de SWAP em SSDs pode diminuir sua vida útil.

Para definir o uso de SWAP quando estiver sobrando 10% de memória RAM, rode o comando abaixo:
```
sudo sysctl -w vm.swappiness=10
```
> Isso significa que a memória RAM precisa estar com 90% capacidade usada, ou seja, 10% restante de espaço livre.


Para persistir esse valor, adicione a linha abaixo no arquivo `/etc/sysctl.d/99-sysctl.conf`
```
vm.swappiness = 10
```

## CPU governor
O utilitário `power profile` presente na distribuição pode não funcionar em alguns processadores AMD, para corrigir rode os comandos abaixo, no terminal:


```
sudo grubby --update-kernel=ALL --args="amd_pstate=active"
```
> Isso irá adicionar a chamada `amd_pstate` no Kernel permitindo o controle de estado da CPU pelo `power profile`.

```
sudo grubby --update-kernel=ALL --remove-args="amd_pstate=passive"
```

> Isso remove o modo `passive`,caso tenha sido adicionado anteriomente.

## Referências
- [AMD P-State EPP can be enabled in Fedora 38 (Kernel 6.3)](https://www.reddit.com/r/Fedora/comments/12d2vs8/amd_pstate_epp_can_be_enabled_in_fedora_38_kernel/)