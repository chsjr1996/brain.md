Devido a um problema no utilitário `pigz` relacionado a biblioteca `zlib-ng` a descompressão das imagens (principalmente das que são muito grandes) acaba falhando devido a um erro de verificação neste processo.

Para contornar temporariamente, basta mudar o utilitário de descompressão para `gzip` da seguinte forma no terminal:
```sh
sudo ln -s /usr/bin/gzip /usr/local/bin/pigz
```
> Isso vai 'enganar' o sistema para utilizar o `gzip` no lugar do `pigz`. Observe que o diretório `/usr/local/bin` não possui o utilitário `pigz`. Ao criar o link simbólico o sistema irá preferir esse diretório e como o `pigz` é na verdade o `gzip` o processo de descompressão deve funcionar.

# Restaurando 'pigz' original
Assim que o problema for corrigido em produção e disponibilizado para sua distribuição Linux, basta executar esse comando no terminal:
```sh
sudo unlink /usr/local/bin/pigz
```

---
> [!tip] Dica
> Isso pode ser usado para outros utilitários/aplicações que apresentem problemas, basta seguir a mesma lógica de usar o `/usr/local/bin` criando um link simbólico para substituir qualquer binário que possa estar apresentando problemas.

> [!NOTE] Referências
> - [Github - Podman issue 23822](https://github.com/containers/podman/issues/23822#issuecomment-2332730697)
