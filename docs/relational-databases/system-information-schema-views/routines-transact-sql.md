---
title: ROTINAs (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- ROUTINES_TSQL
- ROUTINES
dev_langs:
- TSQL
helpviewer_keywords:
- ROUTINES view
- INFORMATION_SCHEMA.ROUTINES view
ms.assetid: c75561b2-c9a1-48a1-9afa-a5896b6454cf
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2e302d454ba0bf243f702b90b24cf7076ed97cb6
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669458"
---
# <a name="routines-transact-sql"></a>ROUTINES (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma linha para cada procedimento armazenado e função que pode ser acessada pelo usuário atual no banco de dados atual. As colunas que descrevem o valor de retorno se aplicam somente a funções. Para procedimentos armazenados, estas colunas terão valor NULL.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de INFORMATION_SCHEMA. *view_name*.  
  
> [!NOTE]  
>  A coluna ROUTINE_DEFINITION contém as instruções originais que criaram a função ou o procedimento armazenado. Estas instruções originais provavelmente conterão retornos de carro inseridos. Se você estiver retornando esta coluna a um aplicativo que exibe os resultados em formato de texto, os retornos de carro embutidos nos resultados de ROUTINE_DEFINITION poderão afetar a formatação do conjunto de resultados geral. Se você selecionar a coluna de ROUTINE_DEFINITION, deverá ajustar os retornos de carro embutidos, por exemplo, retornando o conjunto de resultados em uma grade ou retornando ROUTINE_DEFINITION em sua própria caixa de texto.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|SPECIFIC_CATALOG|**nvarchar (** 128 **)**|Nome específico do catálogo. Este nome é igual a ROUTINE_CATALOG.|  
|SPECIFIC_SCHEMA|**nvarchar (** 128 **)**|Nome específico do esquema.<br /><br /> Importante não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. ** \* \* \* \* ** INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|SPECIFIC_NAME|**nvarchar (** 128 **)**|Nome específico do catálogo. Este nome é igual a ROUTINE_NAME.|  
|ROUTINE_CATALOG|**nvarchar (** 128 **)**|Nome de catálogo da função.|  
|ROUTINE_SCHEMA|**nvarchar (** 128 **)**|Nome do esquema que contém esta função.<br /><br /> Importante não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. ** \* \* \* \* ** INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|ROUTINE_NAME|**nvarchar (** 128 **)**|Nome da função.|  
|ROUTINE_TYPE|**nvarchar (** 20 **)**|Retorna PROCEDURE para procedimentos armazenados e FUNCTION para funções.|  
|MODULE_CATALOG|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|MODULE_SCHEMA|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|MODULE_NAME|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|UDT_CATALOG|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|UDT_SCHEMA|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|UDT_NAME|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|DATA_TYPE|**nvarchar (** 128 **)**|Tipo de dado do valor de retorno da função. Retorna a **tabela** se uma função com valor de tabela.|  
|CHARACTER_MAXIMUM_LENGTH|**int**|Comprimento máximo em caracteres se o tipo de retorno for um tipo de caractere.<br /><br /> -1 para **XML** e dados de tipo de valor grande.|  
|CHARACTER_OCTET_LENGTH|**int**|Comprimento máximo em bytes se o tipo de retorno for um tipo de caractere.<br /><br /> -1 para **XML** e dados de tipo de valor grande.|  
|COLLATION_CATALOG|**nvarchar (** 128 **)**|Sempre retorna NULL.|  
|COLLATION_SCHEMA|**nvarchar (** 128 **)**|Sempre retorna NULL.|  
|COLLATION_NAME|**nvarchar (** 128 **)**|Nome da ordenação do valor de retorno. Para tipos não caractere, retorna NULL.|  
|CHARACTER_SET_CATALOG|**nvarchar (** 128 **)**|Sempre retorna NULL.|  
|CHARACTER_SET_SCHEMA|**nvarchar (** 128 **)**|Sempre retorna NULL.|  
|CHARACTER_SET_NAME|**nvarchar (** 128 **)**|O nome do conjunto de caracteres do valor de retorno. Para tipos não caractere, retorna NULL.|  
|NUMERIC_PRECISION|**smallint**|Precisão numérica do valor de retorno. Para os tipos não numéricos, retorna o NULL.|  
|NUMERIC_PRECISION_RADIX|**smallint**|Precisão numérica da base do valor de retorno. Para tipos não numéricos, retorna NULL.|  
|NUMERIC_SCALE|**smallint**|Escala do valor de retorno. Para tipos não numéricos, retorna NULL.|  
|DATETIME_PRECISION|**smallint**|Precisão fracionária de um segundo se o valor de retorno for do tipo **DateTime**. Caso contrário, retorna NULL.|  
|INTERVAL_TYPE|**nvarchar (** 30 **)**|NULL. Reservado para uso futuro.|  
|INTERVAL_PRECISION|**smallint**|NULL. Reservado para uso futuro.|  
|TYPE_UDT_CATALOG|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|TYPE_UDT_SCHEMA|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|TYPE_UDT_NAME|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|SCOPE_CATALOG|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|SCOPE_SCHEMA|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|SCOPE_NAME|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|MAXIMUM_CARDINALITY|**bigint**|NULL. Reservado para uso futuro.|  
|DTD_IDENTIFIER|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|ROUTINE_BODY|**nvarchar (** 30 **)**|Retorna o SQL para uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] e EXTERNAL para uma função escrita externamente.<br /><br /> Funções sempre serão o SQL.|  
|ROUTINE_DEFINITION|**nvarchar (** 4000 **)**|Retorna os primeiros 4000 caracteres do texto de definição da função ou procedimento armazenado, se a função ou procedimento armazenado não for criptografado. Caso contrário, retorna NULL.<br /><br /> Para garantir que você obtenha a definição completa, consulte a função [OBJECT_DEFINITION](../../t-sql/functions/object-definition-transact-sql.md) ou a coluna definição na exibição de catálogo [Sys. sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) .|  
|EXTERNAL_NAME|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|EXTERNAL_LANGUAGE|**nvarchar (** 30 **)**|NULL. Reservado para uso futuro.|  
|PARAMETER_STYLE|**nvarchar (** 30 **)**|NULL. Reservado para uso futuro.|  
|IS_DETERMINISTIC|**nvarchar (** 10 **)**|Retornará YES se a rotina for determinística.<br /><br /> Retornará NO se a rotina não for determinística.<br /><br /> Sempre retorna NO para procedimentos armazenados.|  
|SQL_DATA_ACCESS|**nvarchar (** 30 **)**|Retorna um dos seguintes valores:<br /><br /> NONE = Função não contém SQL.<br /><br /> CONTAINS = Função possivelmente contém SQL.<br /><br /> READS = Função possivelmente lê dados SQL.<br /><br /> MODIFIES = Função possivelmente modifica dados SQL.<br /><br /> Retorna READS para todas as funções e MODIFIES para todos os procedimentos armazenados.|  
|IS_NULL_CALL|**nvarchar (** 10 **)**|Indica se a rotina será chamada se qualquer um de seus argumentos for NULL.|  
|SQL_PATH|**nvarchar (** 128 **)**|NULL. Reservado para uso futuro.|  
|SCHEMA_LEVEL_ROUTINE|**nvarchar (** 10 **)**|Retorna YES se for uma função de nível de esquema ou NO se não for uma função de nível de esquema.<br /><br /> Sempre retorna YES.|  
|MAX_DYNAMIC_RESULT_SETS|**smallint**|Número máximo de conjuntos de resultados dinâmicos retornado por rotina.<br /><br /> Retorna 0 em caso de funções.|  
|IS_USER_DEFINED_CAST|**nvarchar (** 10 **)**|Retorna YES em caso de função cast definida pelo usuário e NO se não for uma função cast definida pelo usuário.<br /><br /> Sempre retorna NO.|  
|IS_IMPLICITLY_INVOCABLE|**nvarchar (** 10 **)**|Retorna YES se a rotina puder ser invocada implicitamente e NO se função não puder ser invocada implicitamente.<br /><br /> Sempre retorna NO.|  
|CREATED|**datetime**|A hora em que a rotina foi criada.|  
|LAST_ALTERED|**datetime**|A última vez que a função foi modificada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [&#41;sys. Columns &#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys. procedures &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-procedures-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)  
  
  
