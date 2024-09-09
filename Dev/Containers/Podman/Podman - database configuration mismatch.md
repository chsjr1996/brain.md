Este erro pode acontecer devido a criação do diretório de "volumes" com as permissões incorretas. Para corrigir basta remover o diretório e recria-lo manualmente sem executar o podman.

> [!warning] Atenção
> Remover esse diretório pode apagar dados de containers.

Execute no terminal:
```shell
sudo rm -rf ~/.local/share/containers/storage/
```

```shell
mkdir -p ~/.local/share/containers/storage/volumes
```

---

> [!NOTE] Referência
> [Persistent Toolbox error with recent Kinoite releases](https://discussion.fedoraproject.org/t/persistent-toolbox-error-with-recent-kinoite-releases/98180/5)

> [!success] Bug corrigido na versão 5.2.2
> [Github - Container/Podman #23515](https://github.com/containers/podman/issues/23515)
