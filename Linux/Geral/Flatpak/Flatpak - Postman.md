 #linux #flatpak
## Aplicativo não abre e apresenta erro de certificado
Se o aplicativo fechar logo após abrir, e via terminal apresentar algum erro relacionado com certificado/openssl, pode ser que o pacote Flatpak não está conseguindo gerar o arquivo de certificado necessário para o funcionamento do Postman.

No terminal execute os comandos abaixo:
```
cd ~/.var/app/com.getpostman.Postman/config/Postman/proxy
```
> Acessando o diretório onde será armazenado o certificado.

```
openssl req -subj '/C=US/CN=Postman Proxy' -new -newkey rsa:2048 -sha256 -days 365 -nodes -x509 -keyout postman-proxy-ca.key -out postman-proxy-ca.crt
```
> Este comando irá criar os arquivos de certificado necessários.