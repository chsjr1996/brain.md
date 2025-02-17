> [!warning] Atenção
> Ollama pode ser instalado diretamente no sistema, porém esse guia se baseia na instalação via container. Portanto, os comandos que contiverem `<container_cmd>` podem ser representados tanto pelo `docker` ou pelo `podman`, então substitua por um deles.

- [[Ollama - Arch Linux]]
- [[Ollama - Fedora]]

Após isso execute o comando para gerar a especificação CDI:
```sh
sudo nvidia-ctk cdi generate --output=/etc/cdi/nvidia.yaml
```
> Para verificar os nomes dos 'devices' use `nvidia-ctk cdi list`

---
## Nvidia
### Podman
Com podman basta usar o comando abaixo com o parâmetro `--device nvidia.com/gpu=all`, por exemplo:
```sh
podman run -d --device nvidia.com/gpu=all --security-opt=label=disable -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```
> Pode ser necessário passar o parâmetro `--security-opt=label=disable` caso o SELinux esteja presente e ligado.

### Docker
```sh
docker run -d --gpus=all -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama
```

--- 
## AMD
### Podman
```sh
podman run -d --device /dev/kfd --device /dev/dri -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama:rocm
```


> [!tip] Persistindo modelos
> É possível mudar o diretório compartilhado no volume `ollama` acima. Por exemplo, `-v /home/user/.ollama:/root/.ollama`.

### Download de modelos
```sh
<container_cmd> exec -it ollama ollama run llama3.1
```

> [!warning] Atenção
> A versão pode variar, portanto, verificar no site antes qual modelo atual do llama está disponível. Outros modelos podem ser instalados dessa forma.

## Instalação da interface WebUI

### Instalação com NVIDIA
#### Podman
```sh
podman run -d -p 3000:8080 --device nvidia.com/gpu=all --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:cuda
```
#### Docker
```sh
docker run -d -p 3000:8080 --gpus all --add-host=host.docker.internal:host-gateway -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:cuda
```

### Instalação tradicional (sem GPU)
```sh
<container_cmd> run -d --network=host -e OLLAMA_BASE_URL=http://127.0.0.1:11434 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

> [!tip] Persistindo contas
> É adicionar um volume `-v` para persistir as contas adicionadas. Por exemplo, `-v /home/user/.open-webui:/app/backend/data`

## Iniciando e parando os containers
```sh
<container_cmd> start ollama open-webui
```
> Para iniciar.

```sh
<container_cmd> stop ollama open-webui
```
> Para parar.

---
> [!warning] Atenção
> O uso de múltiplos modelos irá acarretar em maior necessidade de processamento além de um consumo excessivo de memória RAM. Use com cautela, e se necessário pare os containers para aliviar a capacidade do hardware.

> [!NOTE] Referências
> - [NVIDIA - CDI support](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/cdi-support.html)
> - [NVIDIA - Podman container toolkit](https://docs.nvidia.com/ai-enterprise/deployment/rhel-with-kvm/latest/podman.html)
