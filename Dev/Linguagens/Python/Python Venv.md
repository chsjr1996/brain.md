#python 

Os ambientes virtuais do Python consistem na criação de um diretório onde serão centralizados todos os pacotes/dependências/bibliotecas para utilização quando ativados. Desta forma, você é capaz de instalar bibliotecas neste diretório sem modificar os diretórios do seu sistema operacional.

## Criando e ativando um  venv
Considerando um ambiente Unix, execute os comandos abaixo em um terminal.
```
mkdir venv
```
> Irá criar um novo diretório chamado `venv`.

```
python -m venv venv
```
> Irá criar um ambiente virtual no diretório `venv`.


Uma vez criado, é necessário ativar o ambiente virtual com o comando abaixo:
```
source venv/bin/activate
```

> [!NOTE] Verificando ativação
> No terminal execute o comando `which python` ou `which python3` para localizar onde o interpretador está instalado. O resultado deve apontar o diretório do venv, garantindo que as bibliotecas e execução do interpretador estejam limitados nesse diretório.
