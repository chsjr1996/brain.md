#mongodb 
## Exportar e importar dados

Para exportar uma cópia da base de dados, use:
```
mongodump -d <database_name> -o <directory_backup>
```

Para importar uma cópia exportada, use:
```
mongorestore -d <database_name> <directory_backup>
```