---
title: CDC. change_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.change_tables
- cdc.change_tables_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.change_tables
ms.assetid: 3525a5f5-8d8b-46a8-b334-4b7cd9fb7c21
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 516a8ddbbd91cb9bd0947d1e1076680430ce9aa4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758716"
---
# <a name="cdcchange_tables-transact-sql"></a>cdc.change_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada tabela de alteração do banco de dados. Uma tabela de alteração é criada quando o Change Data Capture é habilitado em uma tabela de origem. É recomendável não consultar diretamente as tabelas do sistema. Em vez disso, execute o procedimento armazenado [Sys. sp_cdc_help_change_data_capture](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md) .  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID da tabela de alteração. É exclusivo em um banco de dados.|  
|**version**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Para o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], essa coluna sempre retorna 0.|  
|**source_object_id**|**int**|ID da tabela de origem habilitada para Change Data Capture.|  
|**capture_instance**|**sysname**|Nome da instância de captura usada para denominar objetos de controle específicos da instância. Por padrão, o nome é derivado do nome do esquema de origem mais o nome da tabela de origem no formato *schemaname_sourcename*.|  
|**start_lsn**|**binary(10)**|LSN (número de sequência de log) representando o ponto de extremidade inferior na consulta de dados de alteração na tabela de alteração.<br /><br /> NULL = o ponto de extremidade inferior não foi definido.|  
|**end_lsn**|**binary(10)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]<br /><br /> Para o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], essa coluna sempre retorna NULL.|  
|**supports_net_changes**|**bit**|Suporte para consulta de alterações líquidas é habilitado na tabela de alterações.|  
|**has_drop_pending**|**bit**|O processo de captura recebeu notificação que a tabela de origem foi descartada.|  
|**role_name**|**sysname**|Nome da função de banco de dados usada como acesso aos dados de alteração.<br /><br /> NULL = uma função não é usada.|  
|**index_name**|**sysname**|Nome do índice usado para identificar exclusivamente linhas na tabela de origem. **index_name** é o nome do índice de chave primária da tabela de origem ou o nome de um índice exclusivo especificado quando a captura de dados de alteração foi habilitada na tabela de origem.<br /><br /> NULL = a tabela de origem não tinha uma chave primária quando o Change Data Capture foi habilitado e um índice exclusivo não foi especificado quando o Change Data Capture foi habilitado.<br /><br /> Observação: se a captura de dados de alterações estiver habilitada em uma tabela onde existir uma chave primária, o recurso de captura de dados de alterações usará o índice, independentemente de as alterações líquidas estarem habilitadas ou não. Depois que o Change Data Capture estiver habilitado, nenhuma modificação será permitida na chave primária. Se não houver chave primária na tabela, você ainda poderá habilitar o Change Data Capture, mas somente com as alterações líquidas definidas como falsas. Quando o Change Data Capture estiver habilitado, você poderá criar uma chave primária. Você também poderá modificar a chave primária porque o Change Data Capture não usa a chave primária.|  
|**filegroup_name**|**sysname**|Nome do grupo de arquivos no qual a tabela de alteração reside.<br /><br /> NULL = tabela de alteração no grupo de arquivos padrão do banco de dados|  
|**create_date**|**datetime**|Data em que a tabela de origem foi habilitada.|  
|**partition_switch**|**bit**|Indica se o comando **switch Partition** de **ALTER TABLE** pode ser executado em uma tabela habilitada para a captura de dados de alterações. 0 indica que a alternância de partição está bloqueada. As tabelas não particionadas sempre retornam 1.|  
  
## <a name="see-also"></a>Consulte Também  
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)  
  
  
