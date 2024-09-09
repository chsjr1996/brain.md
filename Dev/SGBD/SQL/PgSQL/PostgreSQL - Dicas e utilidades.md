#dbms 

## Alterando sequência (pk increment)
Em determinados cenários pode ser útil alterar o incremento da chave primária. Para fazer isso no PostgreSQL entre com estes comandos no "pgcli":

Verificando o incremento atual
```
SELECT * from <table>_<pk_name>_seq;
```

Alterando o incremento atual
```
SELECT setval('<table>_<pk_name>_seq', <number>, true);
```
> Semelhante ao exemplo anterior substituindo os trechos necessário, onde agora o `<number>` deve ser o próximo incremento desejado.