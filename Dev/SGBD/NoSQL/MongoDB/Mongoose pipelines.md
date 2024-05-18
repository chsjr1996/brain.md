#mongodb
## Agregação
Para executar algo similar à um `inner join` você pode utilizar a função `aggregate`, para isso é necessário montar uma pipeline com as instruções/estágios necessários para correlacionar os documentos entre as collections. Por exemplo:

```javascript
const queryPipeline = [
	{ $match: {  name: { $regex: ".*" + search + ".*", $options: "i" }  } },
	{
	  $lookup: {
		from: ProductCategoryModel.collection.name,
		localField: "category",
		foreignField: "_id",
		as: "category",
	  },
	},
	{
	  $match: {
		"category.active": true,
	  },
	},
	{
	  $unwind: "$category",
	}
]
```

O primeiro `$match` será aplicado para a `Collection` atual. Depois temos o estágio `$lookup` que irá executar a junção (join).

Depois temos um segundo `$match` (opcional) onde é possível aplicar alguma condição na `Collection` correlacionada. No exemplo acima, obter apenas as categorias ativas.

> [!NOTE] Dica
> Em casos de relacionamentos 1:1, o estágio `$unwind` irá converter o resultado de um `array` para `object`.

## Paginação
Para paginação é possível adicionar o estágio `$limit` na pipeline. Porém, pode ser útil/necessário obter a quantidade total de documentos para auxiliar na paginação.

```javascript
let dbCount = await ProductModel.aggregate([...queryPipeline, { $group: { _id: 1, total: { $sum: 1 } } }]);
dbCount = _get(dbCount, '0.total', 0);
```
> Considerando a pipeline do exemplo anterior `queryPipeline`.


```javascript
queryPipeline.push({ $sort: sortConditions });
queryPipeline.push({ $skip: skip });
queryPipeline.push({ $limit: paginationLimit });

const dbDocuments = await ProductModel.aggregate(queryPipeline);
```