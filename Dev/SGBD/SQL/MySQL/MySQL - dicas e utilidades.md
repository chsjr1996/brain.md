#dbms #mysql 
## Duplicando tabela
Pode ser útil para criar um backup ou uma tabela temporária para realizar algum teste em massa. Para isso basta entrar com a seguinte query.

```sql
CREATE TABLE tbl_new AS SELECT * FROM tbl_old;
```

> [!important] Erro 'default value'
> Pode ser que ao tentar fazer isso campos do tipo 'datetime' possam dar errado se não tiverem um valor padrão. Para evitar esse tipo de erro é possível desativar essa validação via query conforme no exemplo abaixo:

```sql
SET SQL_MODE='ALLOW_INVALID_DATES';
```
