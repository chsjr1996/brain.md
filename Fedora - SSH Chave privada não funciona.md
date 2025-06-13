Ao tentar conectar na máquina usando uma chave privada já cadastrada no `authorized_keys` mas mesmo assim pedir senha, confira se:
- O diretório `.ssh` está com as permissões `rwx------` (700)
- Se o arquivo `authorized_keys` e as chaves privadas estão com as permissões `rw-------` (600)
- Se necessário execute o comando do SELinux `restorecon -R ~/.ssh`


---
## Referências
- [Fedora Discussion - SSH pubkey authentication doesn’t work in Fedora 36-37](https://discussion.fedoraproject.org/t/ssh-pubkey-authentication-doesnt-work-in-fedora-36-37/70165)