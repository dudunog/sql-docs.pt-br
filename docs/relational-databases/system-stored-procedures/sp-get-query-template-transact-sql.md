---
title: sp_get_query_template (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_get_query_template
- sp_get_query_template_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_get_query_template
ms.assetid: 85e9bef7-2417-41a8-befa-fe75507d9bf2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 80f5bc86498bc33e0cb04e8ca54154b96307c480
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833215"
---
# <a name="sp_get_query_template-transact-sql"></a>sp_get_query_template (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o formulário com parâmetros de uma consulta. Os resultados retornados imitam o formulário parametrizado de uma consulta que é o resultado do uso de parametrização forçada. sp_get_query_template é usado principalmente quando você cria guias de plano de modelo.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_get_query_template  
   [ @querytext = ] N'query_text'  
   , @templatetext OUTPUT   
   , @parameters OUTPUT   
```  
  
## <a name="arguments"></a>Argumentos  
 '*query_text*'  
 É a consulta para a qual a versão com parâmetros será gerada. '*query_text*' deve estar entre aspas simples e ser precedido pelo especificador N Unicode. N '*query_text*' é o valor atribuído ao @querytext parâmetro. É do tipo **nvarchar (max)**.  
  
 @templatetext  
 É um parâmetro de saída do tipo **nvarchar (max)**, fornecido conforme indicado, para receber a forma parametrizada de *query_text* como um literal de cadeia de caracteres.  
  
 @parameters  
 É um parâmetro de saída do tipo **nvarchar (max)**, fornecido conforme indicado, para receber um literal de cadeia de caracteres dos nomes de parâmetro e tipos de dados que foram parametrizados no @templatetext .  
  
## <a name="remarks"></a>Comentários  
 sp_get_query_template retorna um erro quando ocorre o seguinte:  
  
-   Ele não parametriza nenhum valor literal constante em *query_text*.  
  
-   *query_text* é NULL, não é uma cadeia de caracteres Unicode, sintaticamente inválida ou não pode ser compilada.  
  
 Se sp_get_query_template retornar um erro, ele não modificará os valores dos @templatetext parâmetros de @parameters saída e.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função pública do banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna o formulário com parâmetros de uma consulta que contém dois valores literais constantes.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @my_templatetext nvarchar(max)  
DECLARE @my_parameters nvarchar(max)  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
        FROM Production.ProductModel pm   
        INNER JOIN Production.ProductInventory pi  
        ON pm.ProductModelID = pi.ProductID  
        WHERE pi.ProductID = 2  
        GROUP BY pi.ProductID, pi.Quantity  
        HAVING SUM(pi.Quantity) > 400',  
@my_templatetext OUTPUT,  
@my_parameters OUTPUT;  
SELECT @my_templatetext;  
SELECT @my_parameters;  
```  
  
 Estes são os resultados parametrizados do parâmetro `@my_templatetext``OUTPUT`:  
  
 `select pi . ProductID , SUM ( pi . Quantity ) as Total`  
  
 `from Production . ProductModel pm`  
  
 `inner join Production . ProductInventory pi`  
  
 `on pm . ProductModelID = pi . ProductID`  
  
 `where pi . ProductID = @0`  
  
 `group by pi . ProductID , pi . Quantity`  
  
 `having SUM ( pi . Quantity ) > 400`  
  
 Observe que o primeiro literal constante, `2`, é convertido em um parâmetro. O segundo literal, `400`, não é convertido porque está em uma cláusula `HAVING`. Os resultados retornados por sp_get_query_template imitam o formulário com parâmetros de uma consulta quando a opção PARAMETERIZATION de ALTER DATABASE estiver definida como FORCED.  
  
 Estes são os resultados parametrizados do parâmetro `@my_parameters OUTPUT`:  
  
```  
@0 int  
```  
  
> [!NOTE]  
>  A ordem e a nomeação de parâmetros na saída de sp_get_query_template podem ser alteradas entre atualizações de QFE (Quick Fix Engineering), service pack e de versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. As atualizações também podem fazer com que um conjunto diferente de literais constantes seja parametrizado para a mesma consulta e que um espaçamento diferente seja aplicado nos resultados de ambos os parâmetros de saída.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Especificar comportamento de parametrização de consulta usando guias de plano](../../relational-databases/performance/specify-query-parameterization-behavior-by-using-plan-guides.md)  
  
  
