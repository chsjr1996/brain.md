## Count By
#countby
```csharp
var categoryCounts = products
	.GroupBy(p => p.Category)
	.Select(group => new
	{
		Category = group.Key,
		Count = group.Count()
	});
```
>.NET 8 (lento)

```csharp
var categoryCounts = products
	.CountBy(p => p.Category);
```
>.NET 9 (otimizado)

## Comparando strings
#stringcomparison
```csharp
public bool AreStringsEqual(string first, string second)
{
	return first.ToUpper() == second.ToUpper();
}
```
> Lento

```csharp
public bool AreStringsEqual(string first, string second)
{
	return string.Equals(first, second,
		StringComparison.OrdinalIgnoreCaseee);
}
```
> Rápido

## Converter Enum para String
#enums
```csharp
public stirng GetGreenName()
{
	return Colors.Green.ToString();
}
```
> Lento

```csharp
public stirng GetGreenName()
{
	return nameof(Colors.Green);
}
```
> Rápido

## Ordenação em cadeia
#orderby
```csharp
var result = products
	.OrderBy(item => item.Name)
	.OrderBy(item => item.Price)
	.ToList();
```
> Incoerente, reordena a lista.

```csharp
var result = products
	.OrderBy(item => item.Name)
	.ThenBy(item => item.Price)
	.ToList();
```
> Ordena corretamente. 

## Checagem verdadeira em collections
#collections
```csharp
List<int> numbers = GetNumbers();
bool allPositive = numbers.All(num => num > 0);
```
> Lento

```csharp
List<int> numbers = GetNumbers();
bool allPositive = numbers.TrueForAll(num => num > 0);
```
> Rápido

## Checagem de propriedades em objetos
```csharp
if (product != null &&
   product.Category == "Books" &&
   product.Price > 100)
{
	Console.WriteLine("Offer free shipping");
}
```
> Checagem "extensa"

```csharp
if (product is { Category: "Books", Price: > 100 })
{
	Console.WriteLine("Offer free shipping");
}
```
> Checagem "direta"

## EF Core melhoria de performance nas consultas
```csharp
public List<User> GetUsers()
{
	return db.Users.AsNoTracking().ToList();
}
```

> [!quote] Observações
>  O uso do método `AsNoTracking` pode melhorar a performance, e pode ser usado em cenários de somente leitura, ou seja, os resultados da query não serão escritos no BD diretamente pelo objeto obtido.

---
## Referências
- Jalal Alzebda