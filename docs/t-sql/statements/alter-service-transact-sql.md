---
description: ALTER SERVICE (Transact-SQL)
title: ALTER SERVICE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER SERVICE
- ALTER_SERVICE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- modifying services
- contracts [Service Broker], modifying
- ALTER SERVICE statement
- services [Service Broker], modifying
ms.assetid: 2b4608f7-bb2e-4246-aa29-b52c55995b3a
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 746e1aa7215acd584e6512c3e39fb79014b7821b
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100248"
---
# <a name="alter-service-transact-sql"></a>ALTER SERVICE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera um serviço existente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql 
ALTER SERVICE service_name   
   [ ON QUEUE [ schema_name . ]queue_name ]   
   [ ( < opt_arg > [ , ...n ] ) ]  
[ ; ]  
  
<opt_arg> ::=  
   ADD CONTRACT contract_name | DROP CONTRACT contract_name  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *service_name*  
 É o nome do serviço a ser alterado. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
 ON QUEUE [ _schema_name_**.** ] *queue_name*  
 Especifica a nova fila deste serviço. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] move todas as mensagens deste serviço da fila atual para uma nova fila.  
  
 ADD CONTRACT *contract_name*  
 Especifica um contrato para acrescentar ao conjunto de contratos exposto por este serviço.  
  
 DROP CONTRACT *contract_name*  
 Especifica um contrato a ser excluído do conjunto de contratos exposto por este serviço. O [!INCLUDE[ssSB](../../includes/sssb-md.md)] envia uma mensagem de erro em quaisquer conversas existentes com este serviço que usem este contrato.  
  
## <a name="remarks"></a>Comentários  
 Quando a instrução ALTER SERVICE exclui um contrato de um serviço, o serviço não pode mais ser um destino das conversas que usam esse contrato. Portanto, [!INCLUDE[ssSB](../../includes/sssb-md.md)] não permite conversas novas ao serviço naquele contrato. As conversas existentes que usam o contrato não são afetadas.  
  
 Para alterar a AUTHORIZATION para um serviço, use a instrução ALTER AUTHORIZATION.  
  
## <a name="permissions"></a>Permissões  
 A permissão para alterar um serviço assume como padrão o proprietário do serviço, os membros das funções de banco de dados fixas **db_ddladmin** ou **db_owner** e os membros da função de servidor fixa **sysadmin**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-changing-the-queue-for-a-service"></a>a. Alterando a fila para um serviço  
 O exemplo a seguir altera o serviço `//Adventure-Works.com/Expenses` para usar a fila `NewQueue`.  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    ON QUEUE NewQueue ;  
```  
  
### <a name="b-adding-a-new-contract-to-the-service"></a>B. Adicionando um novo contrato ao serviço  
 O exemplo a seguir altera o serviço `//Adventure-Works.com/Expenses` para permitir caixas de diálogo no contrato `//Adventure-Works.com/Expenses`.  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
### <a name="c-adding-a-new-contract-to-the-service-dropping-existing-contract"></a>C. Adicionando um novo contrato ao serviço, descartando um contrato existente  
 O exemplo a seguir altera o serviço `//Adventure-Works.com/Expenses` para permitir caixas de diálogo no contrato `//Adventure-Works.com/Expenses/ExpenseProcessing` e para não permitir caixas de diálogo no contrato `//Adventure-Works.com/Expenses/ExpenseSubmission`.  
  
```sql  
ALTER SERVICE [//Adventure-Works.com/Expenses]  
    (ADD CONTRACT [//Adventure-Works.com/Expenses/ExpenseProcessing],   
     DROP CONTRACT [//Adventure-Works.com/Expenses/ExpenseSubmission]) ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/create-service-transact-sql.md)   
 [DROP SERVICE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-service-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
