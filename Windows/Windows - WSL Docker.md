# Erro na inicialização
O kernel do WSL2 não suporta a opção `nftables` o que impede a inicialização do Docker.  Para contornar, é possível alternar para a versão legada do `iptables`. No ambiente WSL execute os comandos abaixo:
```shell
sudo update-alternatives --set iptables /usr/sbin/iptables-legacy
```

```shell
sudo update-alternatives --set ip6tables /usr/sbin/ip6tables-legacy
```

> [!NOTE] Referência
> Microsoft Copilot

---
# Inicialização automática
Editar o arquivo `/etc/wsl.conf` e adicionar a seguinte linha na seção `[boot]`:
```
[boot]
...
command="service docker start"
```
