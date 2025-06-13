Exemplo de paginação utilizando o ORM Entity Framework Core.

```csharp
var products = dbContext.Products
	.AsNoTracking()
	.Where(p => p.Category == "Electronics")
	.OrderBy(p => p.ProductId)
	.Skip((pageNumber - 1) * pageSize)
	.Take(pageSize)
	.ToList();
```

SQL gerado:
```sql
SELECT *
FROM Products
WHERE Category = 'Electronics'
ORDER BY ProductId
OFFSET (@pageNumber - 1) * @pageSize ROWS
FETCH NEXT @pageSize ROWS ONLY
```

Exemplo com `pageNumber=3` e `pageSize=100`:
![[csharp_pagination_ef_core.png]]

---
## Referências
- Jalal Alzebda