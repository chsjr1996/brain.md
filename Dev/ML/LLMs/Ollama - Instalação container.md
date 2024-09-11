#ml

Para instalar os modelos compatíveis com

## Instalação base
```sh
podman run -d --device /dev/kfd --device /dev/dri -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama:rocm
```

> [!tip] Persistindo modelos
> É possível mudar o diretório compartilhado no volume `ollama` acima. Por exemplo, `-v /home/user/.ollama:/root/.ollama`.


### Download de modelos
```sh
podman exec -it ollama ollama run llama3.1
```

> [!warning] Atenção
> A versão pode variar, portanto, verificar no site antes qual modelo atual do llama está disponível. Outros modelos podem ser instalados dessa forma.

## Instalação da interface WebUI
```sh
podman run -d --network=host -e OLLAMA_BASE_URL=http://127.0.0.1:11434 -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```

> [!tip] Persistindo contas
> É adicionar um volume `-v` para persistir as contas adicionadas. Por exemplo, `-v /home/user/.open-webui:/app/backend/data`

## Iniciando e parando os containers
```sh
podman start ollama open-webui
```
> Para iniciar.

```sh
podman stop ollama open-webui
```
> Para parar.

---
> [!warning] Atenção
> O uso de múltiplos modelos irá acarretar em maior necessidade de processamento além de um consumo excessivo de memória RAM. Use com cautela, e se necessário pare os container para aliviar a capacidade do hardware.

> [!NOTE] Referências
> - 
