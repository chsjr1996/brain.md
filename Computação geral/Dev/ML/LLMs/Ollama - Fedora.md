 Para instalar o `container toolkit` Fedora (ou RHEL - yum/dnf) basta seguir estes passos:
 
```sh
curl -s -L https://nvidia.github.io/libnvidia-container/stable/rpm/nvidia-container-toolkit.repo | \
  sudo tee /etc/yum.repos.d/nvidia-container-toolkit.repo
```

```sh
sudo dnf install -y nvidia-container-toolkit
```