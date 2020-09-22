---
description: ALTER MESSAGE TYPE (Transact-SQL)
title: ALTER MESSAGE TYPE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_MESSAGE_TYPE_TSQL
- ALTER MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER MESSAGE TYPE statement
- modifying message types
- message types [Service Broker], modifying
ms.assetid: 98c94176-2bdf-4725-b4bc-d33b6b14817d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 21c3ca718321ec94ae1becb5b46aaaa15c653d25
ms.sourcegitcommit: ac9feb0b10847b369b77f3c03f8200c86ee4f4e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90688257"
---
# <a name="alter-message-type-transact-sql"></a>ALTER MESSAGE TYPE (Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  Altera as propriedades de um tipo de mensagem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql 
ALTER MESSAGE TYPE message_type_name  
   VALIDATION =  
    {  NONE   
     | EMPTY   
     | WELL_FORMED_XML   
     | VALID_XML WITH SCHEMA COLLECTION schema_collection_name }  
[ ; ]  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *message_type_name*  
 O nome do tipo de mensagem a ser alterado. Os nomes de servidor, banco de dados e esquema não podem ser especificados.  
  
 VALIDATION  
 Especifica como o [!INCLUDE[ssSB](../../includes/sssb-md.md)] valida o corpo da mensagem para mensagens desse tipo.  
  
 Nenhuma  
 Nenhuma validação é executada. O corpo da mensagem pode conter qualquer dado ou pode ser NULL.  
  
 EMPTY  
 O corpo da mensagem deve ser NULL.  
  
 WELL_FORMED_XML  
 O corpo da mensagem deve conter XML bem formado.  
  
 VALID_XML_WITH_SCHEMA = *schema_collection_name*  
 O corpo da mensagem deve conter XML que obedece a um esquema na coleção de esquema especificada. O *schema_collection_name* precisa ser o nome de uma coleção de esquema XML existente.  
  
## <a name="remarks"></a>Comentários  
 Alterar a validação de um tipo de mensagem não afeta as mensagens que já foram entregues a uma fila.  
  
 Para alterar a AUTHORIZATION para um tipo de mensagem, use a instrução ALTER AUTHORIZATION.  
  
## <a name="permissions"></a>Permissões  
 A permissão para alterar um tipo de mensagem assume como padrão o proprietário do tipo de mensagem, os membros das funções de banco de dados fixas **db_ddladmin** ou **db_owner** e os membros da função de servidor fixa **sysadmin**.  
  
 Quando a instrução ALTER MESSAGE TYPE especifica uma coleção de esquema, o usuário que executa a instrução deve ter a permissão REFERENCES na coleção de esquema especificada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o tipo de mensagem `//Adventure-Works.com/Expenses/SubmitExpense` para exigir que o corpo da mensagem contenha um documento XML bem formado.  
  
```sql  
ALTER MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = WELL_FORMED_XML ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [CREATE MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [DROP MESSAGE TYPE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-message-type-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
