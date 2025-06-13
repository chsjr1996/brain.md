Para acessar um servidor web em uma rede local é necessário liberar o acesso a porta 80 (ou outra que estiver usando) mas regras de firewall.

```sh
sudo firewall-cmd --permanent --add-port=80/tcp
```
> Substituir a porta `80` por outra se necessário.

```sh
sudo firewall-cmd --reload
```

Com isso já deverá ser possível acessar o servidor através da porta liberada no comando acima.