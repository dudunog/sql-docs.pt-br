---
description: Caixa de diálogo Verificar Expressão de Restrição (Visual Database Tools)
title: Caixa de diálogo Expressão de Restrição de Verificação
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.checkconstraintexpression
ms.assetid: beb6ce43-3913-4d66-8826-8e885335b790
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 08bcaa1fa6537268266011b7ea785f9badba54d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497179"
---
# <a name="check-constraint-expression-dialog-box-visual-database-tools"></a>Caixa de diálogo Verificar Expressão de Restrição (Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
Ao anexar uma restrição de verificação a uma tabela ou coluna, é necessário incluir uma expressão SQL. Digite a expressão de restrição de verificação na caixa fornecida.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
Expression  
Insira a expressão  
  
É possível criar uma expressão de restrição simples para verificar dados para uma condição simples ou você pode criar uma expressão complexa, usando operadores Boolianos, para verificar dados para várias condições. Por exemplo, suponha que a tabela de autores tenha uma coluna de código de área onde uma cadeia de caracteres de 5 dígitos é requerida. Esse exemplo de expressão de restrição garante que são permitidos apenas números de 5 dígitos:  
  
```  
zip LIKE '[0-9][0-9][0-9][0-9][0-9]'  
```  
  
Ou, suponha que a tabela de vendas tenha uma coluna chamada quantidade que requer um valor maior que 0. Esse exemplo de expressão de restrição garante que são permitidos apenas valores positivos:  
  
```  
qty > 0  
```  
  
Ou, suponha que a tabela de pedidos limita o tipo de cartões de crédito aceito para todos os pedidos com cartão de crédito. Esse exemplo de expressão de restrição garante que se o pedido for feito com um cartão de crédito, então só Visa, MasterCard, ou American Express são aceitos:  
  
```  
NOT (payment_method = 'credit card') OR  
   (card_type IN ('VISA', 'MASTERCARD', 'AMERICAN EXPRESS'))  
```  
  
## <a name="to-define-a-constraint-expression"></a>Para definir uma expressão de restrição  
Na guia Verificar Restrições das páginas de propriedades, digite uma expressão na caixa de expressão de Restrição que usa a seguinte sintaxe:  
  
```
{constant | column_name | function | (subquery)}  
[{operator | AND | OR | NOT}  
{constant | column_name | function | (subquery)}...]
```
  
A sintaxe de SQL é criada para os seguintes parâmetros:  
  
|Parâmetro|DESCRIÇÃO|  
|-------------|---------------|  
|constante|Um valor literal, como numérico ou dados de caractere. Os dados de caractere devem estar entre aspas (').|  
|column_name|Especifica uma coluna.|  
|função|Uma função interna.|  
|operador|Aritmética, bit a bit, comparação ou operadores de cadeia de caracteres.|  
|AND|Use expressões em Booliano para conectar duas expressões. Os resultados são retornados quando ambas as expressões forem verdadeiras.<br /><br />Quando AND e OR forem ambas usadas em uma instrução, AND é processado primeiro. É possível alterar a ordem de execução usando parênteses.|  
|OU|Use expressões Booleanas para conectar duas ou mais expressões. Os resultados são retornados quando nenhuma das condições for verdadeira.<br /><br />Quando AND e OR forem ambas usadas em uma instrução, OR é avaliado após AND. É possível alterar a ordem de execução usando parênteses.|  
|NOT|Nega qualquer expressão Booleana (que pode incluir palavras-chaves, como LIKE, NULL, BETWEEN, IN e EXISTS).<br /><br />Quando mais de um operador lógico for usado em uma instrução, NOT é processado primeiro. É possível alterar a ordem de execução usando parênteses.|  
  
## <a name="see-also"></a>Consulte Também  
[Restrições exclusivas e restrições de verificação](../../relational-databases/tables/unique-constraints-and-check-constraints.md)  
[Criar restrições exclusivas](../../relational-databases/tables/create-unique-constraints.md)  
  
