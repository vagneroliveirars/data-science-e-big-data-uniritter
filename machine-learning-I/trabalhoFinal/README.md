# Trabalho final: e-commerce

Análise de sentimentos dos reviews da Amazon

Dataset utilizado: reviews_Clothing_Shoes_and_Jewelry_5.json.gz

## Problema abordado

A análise de sentimentos é uma técnica que consiste em extrair informações de textos em linguagem natural. O objetivo dessa técnica é obter, de forma automática, a classificação de um texto ou sentença. Por exemplo, dada uma sentença, um computador classifica-a como positiva ou negativa.

Neste trabalho, essa técnica é aplicada em reviews de produtos da Amazon. O objetivo é saber se o review foi negativo, neutro ou positivo.
  
## Passos realizados na preparação dos dados como entrada para o(s) algoritmo(s) de ML

A base contém 278677 reviews de roupas, sapatos, e jóias.

Exemplo de review:

```json
{
	"_id" : ObjectId("5a10bd4b0caace6a5f644638"),
	"reviewerID" : "A1KLRMWW2FWPL4",
	"asin" : "0000031887",
	"reviewerName" : "Amazon Customer \"cameramom\"",
	"helpful" : [
		0,
		0
	],
	"reviewText" : "This is a great tutu and at a really great price. It doesn't look cheap at all. I'm so glad I looked on Amazon and found such an affordable tutu that isn't made poorly. A++",
	"overall" : 5.0,
	"summary" : "Great tutu-  not cheaply made",
	"unixReviewTime" : 1297468800,
	"reviewTime" : "02 12, 2011"
}
```

Importação dos dados no MongoDB:

```sh
$ mongoimport --db amazon --collection clothing --file Clothing_Shoes_and_Jewelry_5.json
```

Classificação dos dados como positive, negative e neutral no MongoDB:

Negative
```javascript
try {
   db.clothing.updateMany(
      { overall: {$lte: 2.0} },
      { $set: { "classification" : "Negative" } }
   );
} catch (e) {
   print(e);
}
```

Neutral
```javascript
try {
   db.clothing.updateMany(
      { overall: {$eq: 3.0} },
      { $set: { "classification" : "Neutral" } }
   );
} catch (e) {
   print(e);
}
```

Positive
```javascript
try {
   db.clothing.updateMany(
      { overall: {$gt: 3.0} },
      { $set: { "classification" : "Positive" } }
   );
} catch (e) {
   print(e);
}
```

## Notebook com os scripts utilizados:

[NotebookAnaliseSentimentosAmazon.ipynb](NotebookAnaliseSentimentosAmazon.ipynb)
