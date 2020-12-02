---
description: Query with Full-Text Search
title: Consulta com a pesquisa de texto completo | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- queries [full-text search], about full-text queries
- queries [full-text search], predicates
- full-text queries [SQL Server], about full-text queries
- full-text search [SQL Server], querying SQL Server
- full-text queries [SQL Server]
- queries [full-text search], functions
ms.assetid: 7624ba76-594b-4be5-ac10-c3ac4a3529bd
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c34b76e3712dceabf407fcece92f223bb97f1563
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "91867437"
---
# <a name="query-with-full-text-search"></a>Query with Full-Text Search
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
Escreva consultas de texto completo usando os predicados **CONTAINS** e **FREETEXT** e as funções com valor de conjunto de linhas **CONTAINSTABLE** e **FREETEXTTABLE** com uma instrução **SELECT**. Este artigo fornece exemplos de cada predicado e função e ajuda você a escolher o melhor a ser usado.

-   Para corresponder palavras e frases, use **CONTAINS** e **CONTAINSTABLE**.
-   Para corresponder o significado, mas não as palavras exatas, use **FREETEXT** e **FREETEXTTABLE**.

## <a name="examples-of-each-predicate-and-function"></a><a name="examples_simple"></a> Exemplos de cada predicado e função

Os exemplos a seguir usam o banco de dados de exemplo AdventureWorks. Para encontrar a versão final do AdventureWorks, consulte [Bancos de dados e scripts do AdventureWorks para SQL Server 2016 CTP3](https://github.com/microsoft/sql-server-samples/releases/tag/adventureworks). Para executar as consultas de exemplo, você também deve configurar a pesquisa de texto completo. Para mais informações, consulte [Introdução à pesquisa de texto completo](get-started-with-full-text-search.md). 

### <a name="example---contains"></a>Exemplo – CONTAINS  
O exemplo a seguir localiza todos os produtos com um preço de `$80.99` contendo a palavra `"Mountain"`:
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Name, ListPrice  
FROM Production.Product  
WHERE ListPrice = 80.99  
   AND CONTAINS(Name, 'Mountain')  
GO  
```  
  
### <a name="example---freetext"></a>Exemplo – FREETEXT 
 O exemplo a seguir pesquisa todos os documentos que contêm palavras relacionadas a `vital safety components`:
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Title  
FROM Production.Document  
WHERE FREETEXT (Document, 'vital safety components')  
GO  
```

### <a name="example---containstable"></a>Exemplo – CONTAINSTABLE  
 O exemplo a seguir retorna a ID de descrição e a descrição de todos os produtos para os quais a coluna **Description** contém a palavra "aluminum" ao lado da palavra "light" ou "lightweight". Apenas as linhas com classificação 2 ou superior são retornadas.  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT FT_TBL.ProductDescriptionID,  
   FT_TBL.Description,   
   KEY_TBL.RANK  
FROM Production.ProductDescription AS FT_TBL INNER JOIN  
   CONTAINSTABLE (Production.ProductDescription,  
      Description,   
      '(light NEAR aluminum) OR  
      (lightweight NEAR aluminum)'  
   ) AS KEY_TBL  
   ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK > 2  
ORDER BY KEY_TBL.RANK DESC;  
GO  
```  
  
### <a name="example---freetexttable"></a>Exemplo – FREETEXTTABLE  
 O exemplo a seguir estende uma consulta FREETEXTTABLE para retornar primeiro as linhas com classificação mais alta e adicionar a classificação de cada linha à lista de seleção. Para escrever uma consulta semelhante, é necessário saber que **ProductDescriptionID** é a coluna da chave exclusiva para a tabela **ProductDescription**.  
  
```sql 
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
Esta é uma extensão da mesma consulta que retorna apenas as linhas com classificação 10 ou maior:  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT KEY_TBL.RANK, FT_TBL.Description  
FROM Production.ProductDescription AS FT_TBL   
     INNER JOIN  
     FREETEXTTABLE(Production.ProductDescription, Description,  
                    'perfect all-around bike') AS KEY_TBL  
     ON FT_TBL.ProductDescriptionID = KEY_TBL.[KEY]  
WHERE KEY_TBL.RANK >= 10  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  

## <a name="match-words-or-match-meaning"></a>Corresponder palavras ou significado

`CONTAINS`/`CONTAINSTABLE` e `FREETEXT`/`FREETEXTTABLE` são úteis para diferentes tipos de correspondência. As informações a seguir ajudam você a escolher o melhor predicado ou a melhor função para sua consulta:

### <a name="containscontainstable"></a>CONTAINS/CONTAINSTABLE

-   Faça a correspondência de palavras individuais e frases com correspondentes precisos ou difusos (menos precisos).
-   Você também pode fazer o seguinte:
    -   Especifique a proximidade de palavras dentro de uma determinada distância uma da outra.
    -   Retorne correspondências ponderadas.
    -   Combine critérios de pesquisa com operadores lógicos. Para obter mais informações, consulte [Usando operadores boolianos (AND, OR e NOT)](#Using_Boolean_Operators) mais adiante neste artigo.

### <a name="freetextfreetexttable"></a>FREETEXT/FREETEXTTABLE

-   Faça a correspondência de significado, mas não de palavras exatas, palavras especificadas ou frases (a *cadeia de caracteres de texto livre*).
-   As correspondências serão geradas se qualquer termo ou forma de qualquer termo for encontrada no índice de texto completo de uma coluna especificada.

## <a name="compare-predicates-and-functions"></a>Comparar predicados e funções

Os predicados `CONTAINS`/`FREETEXT` e as funções com valor de conjunto de linhas `CONTAINSTABLE`/`FREETEXTTABLE` têm uma sintaxe e opções diferentes. As informações a seguir ajudam você a escolher o melhor predicado ou a melhor função para sua consulta:

### <a name="predicates-contains-and-freetext"></a>Predicados CONTAINS e FREETEXT

**Uso**. Use os **predicados** de texto completo CONTAINS e FREETEXT na cláusula WHERE ou HAVING de uma instrução SELECT.

**Resultados**. Os predicados CONTAINS e FREETEXT retornam um valor TRUE ou FALSE que indica se determinada linha corresponde à consulta de texto completo. As linhas correspondentes são retornadas no conjunto de resultados.

**Mais opções**. Você pode combinar os predicados com qualquer um dos outros predicados [!INCLUDE[tsql](../../includes/tsql-md.md)], como LIKE e BETWEEN.

Especifique se uma única coluna, uma lista de colunas ou todas as colunas da tabela devem ser pesquisadas.

Opcionalmente, você pode especificar o idioma cujos recursos são usados pela consulta de texto completo para a quebra de palavras e lematização, pesquisas no dicionário de sinônimos e remoção de palavras de ruído.

É possível usar um nome de quatro partes no predicado CONTAINS ou FREETEXT para consultar colunas indexadas de texto completo das tabelas de destino em um servidor vinculado. Para preparar um servidor remoto para receber consultas de texto completo, crie um índice de texto completo nas tabelas e colunas de destino no servidor remoto e, em seguida, adicione o servidor remoto como um servidor vinculado.

**Mais informações**. Para obter mais informações sobre a sintaxe e os argumentos desses predicados, consulte [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [FREETEXT](../../t-sql/queries/freetext-transact-sql.md).

### <a name="rowset-valued-functions-containstable-and-freetexttable"></a>Funções com valor de conjunto de linhas CONTAINSTABLE e FREETEXTTABLE

**Uso**. As **funções** de texto completo CONTAINSTABLE e FREETEXTTABLE são iguais a um nome de tabela comum na cláusula FROM de uma instrução SELECT.

Você precisa especificar a tabela base a ser pesquisada ao usar uma dessas funções. Assim como nos predicados, você pode especificar uma única coluna, uma lista de colunas ou todas as colunas da tabela a ser pesquisada e, se preferir, o idioma cujos recursos são usados por uma dada consulta de texto completo.

Normalmente, você precisa unir os resultados de CONTAINSTABLE ou FREETEXTTABLE à tabela base. Para unir as tabelas, é necessário saber o nome de coluna de chave exclusiva. Esta coluna, que ocorre em todas as tabelas habilitadas para texto completo, é usada para impor linhas exclusivas da tabela (a *coluna de chave**exclusiva*). Para obter mais informações sobre a coluna de chave, consulte [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md).

**Resultados**. Essas funções retornam uma tabela de zero, uma ou mais linhas que correspondem à consulta de texto completo. A tabela retornada contém somente as linhas da tabela base que correspondem aos critérios de seleção especificados no critério de pesquisa de texto completo da função.

As consultas que usam uma dessas funções também retornam um valor de classificação de relevância (RANK) e uma chave de texto completo (KEY) para cada linha retornada, da seguinte maneira:

-   Coluna **KEY**. A coluna KEY retorna valores exclusivos das linhas retornadas. A coluna KEY pode ser usada para especificar critérios de seleção.
-   Coluna **RANK**. A coluna RANK retorna um *valor de classificação* para cada linha que indica o grau de correspondência da linha com os critérios de seleção. Quanto mais alto o valor de classificação do texto ou documento em uma linha, mais relevante será a linha para a consulta de texto completo especificada. Diferentes linhas podem ter a mesma classificação. É possível limitar o número de correspondências a serem retornadas especificando o parâmetro opcional *top_n_by_rank* . Para obter mais informações, veja [Limitar resultados da pesquisa com RANK](../../relational-databases/search/limit-search-results-with-rank.md).

**Mais informações**. Para obter mais informações sobre a sintaxe e os argumentos dessas funções, consulte [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md).

## <a name="specific-types-of-searches"></a><a name="examples_specific"></a> Tipos específicos de pesquisas

###  <a name="search-for-a-specific-word-or-phrase-simple-term"></a><a name="Simple_Term"></a> Pesquisar uma palavra ou frase específica (Termo Simples)  
 Você pode usar [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)ou [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) para pesquisar uma tabela para uma frase ou palavra específica. Por exemplo, para pesquisar a tabela **ProductReview** no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e localizar todos os comentários sobre um produto com a frase “curva de aprendizado”, use o predicado CONTAINS, da seguinte forma:  
  
```sql
USE AdventureWorks2012  
GO  
  
SELECT Comments  
FROM Production.ProductReview  
WHERE CONTAINS(Comments, '"learning curve"')  
GO  
```  
  
O critério de pesquisa, nesse caso, “curva de aprendizado”, pode ser complexo, podendo consistir em um ou mais termos.

#### <a name="more-info-about-simple-term-searches"></a>Mais informações sobre pesquisas de termo simples

Na pesquisa de texto completo, uma *palavra* (ou *token*) é uma cadeia de caracteres cujos limites são identificados pelas quebras de palavras apropriadas, seguindo as regras linguísticas do idioma especificado. Uma *frase* válida consiste em várias palavras, com ou sem sinais de pontuação entre elas.

Por exemplo, "croissant" é uma palavra e "café com leite" é uma frase. Palavras e frases como essas são chamadas de termos simples.

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) procuram uma correspondência exata da frase. [FREETEXT](../../t-sql/queries/freetext-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) desmembram a frase em palavras separadas.

###  <a name="search-for-a-word-with-a-prefix-prefix-term"></a><a name="Prefix_Term"></a> Pesquisar uma palavra com um prefixo (Termo de Prefixo)  
 Você pode usar [CONTAINS](../../t-sql/queries/contains-transact-sql.md) ou [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) para procurar palavras ou frases com um prefixo especificado. Todas as entradas na coluna que contêm o texto que começa com o prefixo especificado são retornadas. Por exemplo, para procurar todas as linhas que contêm o prefixo `top`-, como em `top``ple`, `top``ping`e `top`. A consulta será semelhante ao exemplo a seguir:  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description, ProductDescriptionID  
FROM Production.ProductDescription  
WHERE CONTAINS (Description, '"top*"' )  
GO  
```  
  
 Todo texto que corresponder ao texto especificado antes do asterisco (*) será retornado. Se o texto e o asterisco não forem delimitados por aspas duplas, como em `CONTAINS (DESCRIPTION, 'top*')`, a pesquisa de texto completo não considerará o asterisco como sendo um curinga.  
  
 Quando o termo de prefixo for uma frase, todos os tokens que constituírem a frase serão considerados termos de prefixo separados. Todas as linhas que têm palavras que começam com os termos de prefixo serão retornadas. Por exemplo, o prefixo "pão light\*" encontrará linhas com o texto "pãozinho light" ou "pão light", mas não retornará "pão torrado light."

#### <a name="more-info-about-prefix-searches"></a>Mais informações pesquisas de prefixo

Um *termo de prefixo* refere-se a uma cadeia de caracteres colocada na frente de uma palavra para gerar uma palavra derivada ou uma forma flexionada.

-   Para um único termo de prefixo, qualquer palavra que comece com o termo especificado fará parte do conjunto de resultados. Por exemplo, o termo "auto*" retorna "automático", "automóvel" e assim por diante.

-   Para uma frase, cada palavra é considerada um termo de prefixo. Por exemplo, o termo “trans auto\*” corresponde a “transmissão automática” e “transdutor de automóvel”, mas não corresponde a “transmissão de motor automática”.

Pesquisas de prefixo são compatíveis com [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md).
  
###  <a name="search-for-inflectional-forms-of-a-specific-word-generation-term"></a><a name="Inflectional_Generation_Term"></a> Pesquisar as formas flexionadas de uma palavra específica (Termo de Geração)  
Você pode usar [CONTAINS](../../t-sql/queries/contains-transact-sql.md), [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md), [FREETEXT](../../t-sql/queries/freetext-transact-sql.md)ou [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) para procurar todos os diferentes tempos e conjugações de um verbo ou ambas as formas, singular e plural, de um substantivo (uma pesquisa flexionada) ou sinônimos de uma palavra específica (uma pesquisa de dicionário de sinônimos).  
  
O exemplo a seguir pesquisa qualquer forma de “pé" ("pé", "pés" e assim por diante) na coluna `Comments` da tabela `ProductReview` do banco de dados `AdventureWorks`: 
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Comments, ReviewerName  
FROM Production.ProductReview  
WHERE CONTAINS (Comments, 'FORMSOF(INFLECTIONAL, "foot")')  
GO  
```  
  
A pesquisa de texto completo usa *lematizadores*, que permitem pesquisar os diferentes tempos e conjugações de um verbo ou as formas singular e plural de um substantivo. Para obter mais informações sobre lematizadores, veja [Configurar e gerenciar separadores de palavras e lematizadores para pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  

#### <a name="more-info-about-generation-term-searches"></a>Mais informações sobre pesquisas de termo de geração

As *formas flexionadas* são os diferentes tempos e conjugações de um verbo ou as formas singular e plural de um substantivo.

Por exemplo, pesquise a forma flexionada da palavra "dirigir". Se várias linhas da tabela contivessem as palavras "dirigir", "dirige", "dirigiu", "dirigindo" e "dirigido", todas elas fariam parte do conjunto de resultados, pois cada uma delas seria uma flexão gerada da palavra dirigir.

Por padrão,[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) procuram termos flexionados de todas as palavras especificadas. [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) são compatíveis com um argumento `INFLECTIONAL` opcional.

### <a name="search-for-synonyms-of-a-specific-word"></a>Pesquisar sinônimos de uma palavra específica

Um *dicionário de sinônimos* define sinônimos especificados pelo usuário para os termos. Para obter mais informações sobre arquivos de dicionário de sinônimos, consulte [Configurar e gerenciar arquivos do dicionário de sinônimos na pesquisa de texto completo](../../relational-databases/search/configure-and-manage-thesaurus-files-for-full-text-search.md).

Por exemplo, se uma entrada "{carro, automóvel, caminhão, van}" for adicionada ao dicionário de sinônimos, será possível pesquisar o sinônimo da palavra "carro". Todas as linhas da tabela consultada que contiverem as palavras "automóvel", "caminhão", "van" ou "carro" serão exibidas no conjunto de resultados, pois cada uma dessas palavras pertence a um conjunto de expansão de sinônimos contendo a palavra "carro".

[FREETEXT](../../t-sql/queries/freetext-transact-sql.md) e [FREETEXTTABLE](../../relational-databases/system-functions/freetexttable-transact-sql.md) usam o dicionário de sinônimos por padrão. [CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) são compatíveis com um argumento `THESAURUS` opcional.

### <a name="search-for-a-word-near-another-word"></a>Pesquisar uma palavra NEAR (próxima) a outra palavra

Um *termo de proximidade* indica palavras ou frases que estão perto umas das outras. Você também pode especificar o número máximo de condições não relacionadas à pesquisa que separam a primeira e a última condição da pesquisa. Além disso, você pode pesquisar palavras ou frases em qualquer ordem, ou na ordem em que as especificar.

Por exemplo, você quer localizar as linhas em que a palavra "gelo" esteja perto de "hóquei" ou em que a frase "patinação no gelo" esteja perto da frase "hóquei no gelo". 

[CONTAINS](../../t-sql/queries/contains-transact-sql.md) e [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md)

Para obter mais informações sobre pesquisas de proximidade, consulte [Pesquisar palavras perto de outra palavra com NEAR](search-for-words-close-to-another-word-with-near.md).

###  <a name="search-for-words-or-phrases-using-weighted-values-weighted-term"></a><a name="Weighted_Term"></a> Pesquisar palavras ou frases usando valores ponderados (Termo Ponderado)  
Você pode usar [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md) para procurar palavras ou frases e especificar um valor ponderado. A ponderação, medida como um número de 0,0 a 1,0, indica a importância de cada palavra e frase em um conjunto de palavras e frases. Um peso 0,0 é o mais baixo, e um peso 1,0 é o mais alto.  
  
O exemplo a seguir mostra uma consulta que procura todos os endereços de clientes usando pesos, em que qualquer texto que comece com a cadeia de caracteres "Baía" tem também "Rua" ou "Vista". Os resultados dão uma classificação mais alta a essas linhas que contêm mais das palavras especificadas.  
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT AddressLine1, KEY_TBL.RANK   
FROM Person.Address AS Address INNER JOIN  
CONTAINSTABLE(Person.Address, AddressLine1, 'ISABOUT ("Bay*",   
         Street WEIGHT(0.9),   
         View WEIGHT(0.1)  
         ) ' ) AS KEY_TBL  
ON Address.AddressID = KEY_TBL.[KEY]  
ORDER BY KEY_TBL.RANK DESC  
GO  
```  
  
 Um termo ponderado pode ser usado junto com qualquer termo simples, termo de prefixo, termo de geração ou termo de proximidade.

#### <a name="more-info-about-weighted-term-searches"></a>Mais informações sobre pesquisas de termo ponderado

Em uma pesquisa de termo ponderado, um *valor de ponderação* indica o grau de importância de cada palavra e frase em um conjunto de palavras e frases. Um valor ponderado de 0,0 é o mais baixo e um valor ponderado de 1,0 é o mais alto.

Por exemplo, em uma consulta que pesquisa vários termos, é possível atribuir a cada palavra da pesquisa um valor equilibrado indicando sua importância com relação às demais palavras da pesquisa. O resultado desse tipo de consulta retorna primeiro as linhas mais relevantes, de acordo com o peso relativo atribuído às palavras da pesquisa. Os conjuntos de resultados contêm documentos ou linhas que, por sua vez, contêm qualquer um dos termos especificados (ou conteúdo entre eles); todavia, alguns resultados serão considerados mais relevantes do que outros devido à variação dos valores ponderados associados aos diferentes termos de pesquisa.

Pesquisas de termo ponderado são compatíveis com [CONTAINSTABLE](../../relational-databases/system-functions/containstable-transact-sql.md).

##  <a name="use-and-or-and-not-boolean-operators"></a><a name="Using_Boolean_Operators"></a> Usar AND, OR e NOT (operadores boolianos)
 
O predicado CONTAINS e a função CONTAINSTABLE usam as mesmas condições de pesquisa. Os dois permitem combinar vários termos de pesquisa usando operadores boolianos – AND, OR e NOT – para executar operações lógicas. Você pode usar AND, por exemplo, para localizar linhas que contêm “expresso” e “rosca”. Você pode usar AND NOT, por exemplo, para localizar as linhas que contêm "rosca", mas que não contêm "cream cheese".  
  
Por outro lado, FREETEXT e FREETEXTTABLE tratam os termos boolianos como palavras a serem pesquisadas.  
  
 Para obter mais informações sobre como combinar CONTAINS com outros predicados que usam os operadores lógicos AND, OR e NOT, veja [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir usa o predicado CONTAINS para pesquisar descrições nas quais a ID de descrição não é igual a 5 e a descrição contém as palavras “Alumínio” e “eixo”. O critério de pesquisa usa o operador booliano AND. Esse exemplo usa a tabela ProductDescription do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
USE AdventureWorks2012  
GO  
  
SELECT Description  
FROM Production.ProductDescription  
WHERE ProductDescriptionID <> 5 AND  
   CONTAINS(Description, 'aluminum AND spindle')  
GO  
```  
  
##  <a name="case-stopwords-language-and-thesaurus"></a><a name="Additional_Considerations"></a> Maiúsculas e minúsculas, palavras irrelevantes, idioma e dicionário de sinônimos

 Ao escrever consultas de texto completo, você também poderá especificar as opções a seguir:
  
-   **Diferenciação de maiúsculas e minúsculas**. As consultas de pesquisa de texto completo não diferenciam maiúsculas de minúsculas. No entanto, em japonês há várias ortografias fonéticas em que o conceito de normalização ortográfica é parecido à não diferenciação de maiúsculas e minúsculas (por exemplo, kana = não diferenciação). Esse tipo de normalização ortográfica não tem suporte.  

-   **Palavras irrelevantes**. Ao definir uma consulta de texto completo, o Mecanismo de Texto Completo descarta as palavras irrelevantes (também chamadas de palavras de ruído) dos critérios de pesquisa. Palavras irrelevantes são palavras como "um", "e", "é" ou "o(s)/a(s)", que podem ocorrer com frequência, mas normalmente não ajudam na pesquisa de um determinado texto. As palavras irrelevantes são relacionadas em uma lista de palavras irrelevantes (stoplist). Cada índice de texto completo é associado a uma lista de palavras irrelevantes específica, que determina quais palavras irrelevantes são omitidas da consulta ou do índice no momento da indexação. Para obter mais informações, consulte [Configurar e gerenciar palavras irrelevantes e listas de palavras irrelevantes na pesquisa de texto completo](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  

-   **Idioma**, com a opção **LANGUAGE**. Muitos termos de consulta dependem bastante do comportamento do separador de palavras. Para assegurar que você use o separador de palavras (e lematizador) e o arquivo de dicionário de sinônimos corretos, é recomendável especificar a opção LANGUAGE. Para obter mais informações, veja [Escolher um idioma ao criar um índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
-   **Dicionário de sinônimos**. As consultas FREETEXT e FREETEXTTABLE usam o dicionário de sinônimos por padrão. CONTAINS e CONTAINSTABLE suportam um argumento THESAURUS opcional. Para obter mais informações, consulte [Configurar e gerenciar arquivos do dicionário de sinônimos na pesquisa de texto completo](configure-and-manage-thesaurus-files-for-full-text-search.md).
  
##  <a name="check-the-tokenization-results"></a><a name="tokens"></a> Verificar os resultados da geração de tokens

Depois de aplicar determinada combinação de separador de palavras, dicionário de sinônimos e lista de palavras irrelevantes a uma consulta, você poderá ver como a pesquisa de texto completo gera tokens dos resultados usando a exibição de gerenciamento dinâmico **sys.dm_fts_parser**. Para obter mais informações, veja [sys.dm_fts_parser &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-parser-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)   
 [CONTAINSTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/containstable-transact-sql.md)   
 [FREETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/freetext-transact-sql.md)   
 [FREETEXTTABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/freetexttable-transact-sql.md)   
 [Criar consultas de pesquisa de texto completo &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-full-text-search-queries-visual-database-tools.md)   
 [Melhorar o desempenho de consultas de texto completo](../../relational-databases/search/improve-the-performance-of-full-text-queries.md)
