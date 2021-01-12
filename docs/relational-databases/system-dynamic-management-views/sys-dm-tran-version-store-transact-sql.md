---
description: sys.dm_tran_version_store (Transact-SQL)
title: sys.dm_tran_version_store (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_TSQL
- sys.dm_tran_version_store
- dm_tran_version_store
- dm_tran_version_store_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a85bd124db2e6308f4c09b306e89c6e92a4d7b20
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98101386"
---
# <a name="sysdm_tran_version_store-transact-sql"></a>sys.dm_tran_version_store (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma tabela virtual que exibe todos os registros de versão no repositório de versão. o **Sys.dm_tran_version_store** não é eficiente para ser executado porque consulta todo o repositório de versão, e o repositório de versão pode ser muito grande.  
  
 Cada registro com controle de versão é armazenado como dados binários juntamente com algumas informações de rastreamento ou de status. Semelhante a registros em tabelas de banco de dados, os registros de armazenamento de versão são armazenados em páginas de 8.192 bytes. Se um registro exceder 8.192 bytes, ele será dividido em dois registros diferentes.  
  
 Porque o registro com controle de versão é armazenado como binário, não há nenhum problema com ordenações diferentes de bancos de dados diferentes. Use **Sys.dm_tran_version_store** para localizar as versões anteriores das linhas na representação binária, pois elas existem no repositório de versão.  
  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.dm_tran_version_store  
```  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|Número de sequência da transação que gera a versão de registro.|  
|**version_sequence_num**|**bigint**|Número de sequência da versão de registro. Este valor é exclusivo dentro da transação que gera a versão.|  
|**database_id**|**int**|ID do banco de dados do registro com controle de versão.|  
|**rowset_id**|**bigint**|ID do conjunto de linhas do registro.|  
|**status**|**tinyint**|Indica se um registro com controle de versão foi dividido em dois registros. Se o valor for 0, o registro será armazenado em uma página. Se o valor for 1, o registro será dividido em dois registros armazenados em duas páginas diferentes.|  
|**min_length_in_bytes**|**smallint**|Comprimento mínimo do registro em bytes.|  
|**record_length_first_part_in_bytes**|**smallint**|Comprimento em bytes da primeira parte do registro com controle de versão.|  
|**record_image_first_part**|**varbinary(8000)**|Imagem binária da primeira parte do registro com controle de versão.|  
|**record_length_second_part_in_bytes**|**smallint**|Comprimento em bytes da segunda parte do registro com controle de versão.|  
|**record_image_second_part**|**varbinary(8000)**|Imagem binária da segunda parte do registro com controle de versão.|  
  
## <a name="permissions"></a>Permissões

Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa um cenário de teste no qual quatro transações simultâneas, cada uma identificada por um XSN (número de sequência de transação), estão sendo executadas em um banco de dados no qual as opções ALLOW_SNAPSHOT_ISOLATION e READ_COMMITTED_SNAPSHOT estão definidas como ON. As seguintes transações estão sendo executadas:  
  
-   XSN-57 é uma operação de atualização sob o isolamento serializável.  
  
-   XSN-58 é o mesmo que XSN-57.  
  
-   XSN-59 é uma operação de seleção em isolamento de instantâneo.  
  
-   XSN-60 é o mesmo que XSN-59.  
  
 A consulta a seguir é executada.  
  
```  
SELECT  
    transaction_sequence_num,  
    version_sequence_num,  
    database_id rowset_id,  
    status,  
    min_length_in_bytes,  
    record_length_first_part_in_bytes,  
    record_image_first_part,  
    record_length_second_part_in_bytes,  
    record_image_second_part  
  FROM sys.dm_tran_version_store;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num version_sequence_num database_id  
------------------------ -------------------- -----------  
57                      1                    9             
57                      2                    9             
57                      3                    9             
58                      1                    9             
  
rowset_id            status min_length_in_bytes  
-------------------- ------ -------------------  
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038386688    0      16                   
  
record_length_first_part_in_bytes  
---------------------------------  
29                                 
29                                 
29                                 
33                                 
  
record_image_first_part                                               
--------------------------------------------------------------------  
0x50000C0073000000010000000200FCB000000001000000270000000000          
0x50000C0073000000020000000200FCB000000001000100270000000000          
0x50000C0073000000030000000200FCB000000001000200270000000000          
0x500010000100000002000000030000000300F800000000000000002E0000000000  
  
record_length_second_part_in_bytes record_image_second_part  
---------------------------------- ------------------------  
0                                  NULL  
0                                  NULL  
0                                  NULL  
0                                  NULL  
```  
  
 A saída mostra que XSN-57 criou três versões de linha de uma tabela e XSN-58 criou uma versão da linha de outra tabela.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
