
## Funcionalidades
- [x] Mensagens em tempo real
- [x] Canais de socket privados
- [x] Busca por usuários para iniciar novas conversas
- [x] Filtrar chats pelo nome da sala (nome do usuário ou grupo)
- [ ] Mostrar quando o usuário está digitando `*(1)`
- [ ] Mostrar quando o usuário está online `*(2)`
- [ ] Mensagens em grupos `*(3)`
- [ ] Anexar imagens
- [ ] Buscar por mensagens para encontrar conversas
- [ ] Encaminhar mensagens
- [ ] Favoritar mensagens
- [ ] Editar mensagens (próprias, ou geral para admin de grupos)
- [ ] Apagar mensagens (própria e de outros)
- [ ] Reações nas mensagens
- [ ] Bloquear usuários
- [ ] ???

### Observações
- 1. delay precisa ser melhorado quando a mensagem é enviada
	- 1.1 precisar ser melhorado em conversas em grupo
- 2. só está funcionando na tela da conversa, 'presence' precisa ser movido de forma global na aplicação
	- 2.2 ainda precisa de funcionalidade para ocultar status online
- 3. funciona, mas ainda não é possível criar grupos
	- 3.3 precisa mostrar membros em uma tela separada para gestão

---
## Correções e ajustes gerais
### Backend
- [x] Corrigir autenticação em `routes/channels.php`
- [ ] Criar novas rotas:
  - [ ] pessoas (lista de usuários para iniciar uma nova conversa/sala)
      - [ ] permitir ver quem está online/offline
      - [ ] exibir total de usuários online
      - [x] conversas/salas (lista de conversas já iniciadas)
- [ ] permitir anexar imagens e enviar emojis nas mensagens
- [ ] usar fila para processar mensagens e persistir no BD (ingest/diggest)
- [ ] ...?
  
### Frontend
- [ ] Refatorar:
	 - [x] Criar service para AppChat/sendMessage
	 - [x] Criar service para AppChat/onMounted get messages
	 - [ ] ...???
- [x] Acrescentar tipagem no componente do chat
- [ ] Melhorar visual do chat:
	- [x] scroll apenas no container do chat não na tela inteira  
	- [x] disposição do componente 'digitando';  
	- [x] mostrar se usuário está online/offline;  
	- [ ] permitir criar grupos de conversa (adicionar mais de um usuário na conversa);  
	- [ ] permitir anexar imagens e enviar emojis nas mensagens;  
- [ ] Adicionar i18n  
- [ ] Adicionar novos itens de menu:  
	- [ ] pessoas (lista de usuários)  
	- [x] mensagens (lista de conversas já iniciadas)  
- [ ] dashboard (refazer)  
- [x] permitir criar novas conversas/salas (1:1 ou grupo)  
- [ ] permitir ver quem está online/offline  
- [x] conversas/salas (lista de conversas já iniciadas)  
- [ ] ...?
