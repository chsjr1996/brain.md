#ml

Os comandos a seguir representam a instalação 
```
podman run -d --device /dev/kfd --device /dev/dri -v ollama:/root/.ollama -p 11434:11434 --name ollama ollama/ollama:rocm
```

```
podman exec -it ollama ollama run llama
```

```
podman run -d --network=host -e OLLAMA_BASE_URL=[http://127.0.0.1:11434](http://127.0.0.1:11434/) -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main
```
