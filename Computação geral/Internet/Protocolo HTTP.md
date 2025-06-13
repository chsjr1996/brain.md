HTTP (Hypertext Transfer Protocol) é um protocolo usado para transmitir hipertexto pela World Wide Web. Ele define como as mensagens são formatadas e transmitidas, e como servidores web e navegadores devem responder a vários comandos. 

O HTTP opera em um modelo de solicitação-resposta: um cliente (geralmente um navegador web) envia uma solicitação HTTP a um servidor para obter recursos, como páginas web ou arquivos, e o servidor responde com o conteúdo solicitado e um código de status HTTP indicando o resultado da solicitação. 

O HTTP é sem estado, o que significa que cada solicitação de um cliente para um servidor é independente e não retém informações sobre interações anteriores. Ele forma a base da comunicação de dados na web e é normalmente usado com HTTP seguro (HTTPS) para comunicação criptografada.

## Verbos HTTP
Requisições HTTP são representadas por uma URL e um verbo, podendo também conter parâmetros ou informações encapsuladas. Segue abaixo alguns exemplos de verbos:

### GET
O mais comum, e é utilizado para obter informações de uma determinada URL. Toda ação básica de um navegador com acessar um site ou um link geralmente utiliza este verbo.

Este tipo de requisição pode enviar parâmetros na URL, por exemplo:

`GET /api/posts?status=active&visibility=public`

Neste caso os parâmetros são `status` e `visibility` seguido de seus valores `active` e  `public` respectivamente. O servidor poderá capturar esses parâmetros, que geralmente são utilizados como filtro no retorno da resposta.

> [!Quote] Observação
> Embora seja possível enviar um corpo/body na requisição, este verbo não é adequado para isto, devendo usar o POST para essa finalidade.

> [!Warning] Atenção
> Nunca utilize esse verbo para transportar informações sensíveis, principalmente relacionadas à login, como usuário e senha. O Post é mais apropriado, pois envia isso no corpo da requisição, de forma encapsulada e encriptada utilizando SSL.

### POST
Utilizado para transportar informações para o servidor, como criação de um usuário, ou post, que contem dados sobre essas entidades.

### PUT
Utilizado para atualizar alguma entidade.

### PATCH
Utilizado para atualizar alguma entidade, porém parcialmente, ou seja, apenas algum dado específico.

### DELETE
Utilizado para deletar alguma entidade

### HEAD

### OPTIONS

### TRACE

### CONNECT


---
## Referências
- [Roadmap.sh - Backend](https://roadmap.sh/backend)