**Proposta básica** para gestão de finanças com base no template de despesas pessoal.

# Bibliotecas
- [Filament PHP](https://filamentphp.com/docs)

# Tabelas
## Lançamentos
Colunas:
- descrição
- dia de pagamento
- dia de vencimento
- valor
- forma de pagamento (saldo/débito, crédito)
- parcela (1/4, 2/4, etc...)

## Compras

### Grupo/lista
- nome
- data (created_at adicional)

### itens do grupo/lista
- descrição
- quantidade
- valor

## Contas
- nome
- saldo

## Cartões de crédito
- nome
- limite
- fatura atual
- anuidade

---

# Funcionalidades
- listar despesas separadas por mês de Janeiro até Dezembro do ano atual
- dashboard de saúde financeira
	- gráficos ou cards por categoria de gastos
	- gráficos de economias
	- resumo dos meses do ano atual (total de despesas e saldo de cada mês)