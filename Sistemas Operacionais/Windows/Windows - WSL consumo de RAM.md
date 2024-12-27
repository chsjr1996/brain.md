É necessário limitar a quantidade máxima de RAM do WSL, para isso crie um arquivo na raiz do usuário Windows chamado `.wslconfig` contendo as seguintes linhas:
```
[wsl2]
memory=4GB
processors=8
```
> A quantidade mínima recomendada para trabalhar com Node.JS é 4GB, portanto se for utilizá-lo considere este tamanho mínimo para o WSL.
