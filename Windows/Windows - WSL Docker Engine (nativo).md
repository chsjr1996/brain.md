É possível instalar o [[Docker]] dentro do WSL, sem depender do Docker Desktop. Para isto basta entrar no `wsl` e instalar com o comando abaixo:

Preparando e adicionando o repositório:
```sh
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Instalando o Docker Engine:
```sh
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

# Inicialização automática
Editar o arquivo `/etc/wsl.conf` e adicionar a seguinte linha na seção `[boot]`:
```
[boot]
...
command="service docker start"
```

---

> [!NOTE] Referências
> - [Github - codeedu/wsl2-docker-quickstart](https://github.com/codeedu/wsl2-docker-quickstart?tab=readme-ov-file#4-docker-engine-docker-nativo-diretamente-instalado-no-wsl2)
> - [Docker Docs - Ubuntu Install](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)
