
## Comandos básicos

## Manipulação de arquivos

| Comando                   | Descrição                                                     |
| ------------------------- | ------------------------------------------------------------- |
| ls                        | lista diretórios                                              |
| ls -al                    | lista formatada com diretórios ocultos                        |
| cd /path/dir              | acessa um diretório                                           |
| cd                        | retorna ao diretório 'home'                                   |
| pwd                       | mostra o diretório atual                                      |
| mkdir /path/dir           | cria um diretório                                             |
| mkdir -p                  | cria um subdiretórios mesmo quando diretório 'pai' não existe |
| rm /path/file             | deleta um arquivo                                             |
| rm -r /path/file_or_dir   | deleta um arquivo ou diretório recursivamente                 |
| tar cf destfile.tar files | compacta arquivos                                             |
| tar xf file.tar           | descompacta arquivos                                          |
| tar tf file.tar           | mostra conteúdo que estão compactados                         |

---
## SSH

| Comando                             | Descrição                              |
| ----------------------------------- | -------------------------------------- |
| ssh user@host                       | conecta em um servidor ssh com usuário |
| ssh -p port user@host               | conecta especificando uma porta        |
| ssh -i /path/key user@host          | conecta usando uma chave privada       |
| ssh -o IdentitiesOnly=yes user@host | conecta usando apenas identidade       |

---
## Rede

---

## Informações do sistema

