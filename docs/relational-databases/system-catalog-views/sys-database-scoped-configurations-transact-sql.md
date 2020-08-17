---
description: sys. database_scoped_configurations (Transact-SQL)
title: sys. database_scoped_configurations (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- database_scoped_configurations
- database_scoped_configurations_TSQL
- sys.database_scoped_configurations
- sys.database_scoped_configurations_TSQL
helpviewer_keywords:
- sys.database_scoped_configurations catalog view
ms.assetid: 8899310a-3464-4d38-9f2f-88396c4e7dc2
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current||= azure-sqldw-latest
ms.openlocfilehash: 6edd7864c127ea068e3017c7aa26ad5be86a4c8a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88323242"
---
# <a name="sysdatabase_scoped_configurations-transact-sql"></a>sys. database_scoped_configurations (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-addw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

Contém uma linha por configuração. 

|Nome da coluna|Tipo de dados|Descrição|
|-----------------|---------------|-----------------|
|**configuration_id**|**int**|ID da opção de configuração.|
|**name**|**nvarchar(60)**|O nome da opção de configuração. Para obter informações sobre as configurações possíveis, consulte [ALTER DATABASE Scoped CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).|
|**value**|**sqlvariant**|O valor definido para esta opção de configuração para a réplica primária.|
|**value_for_secondary**|**sqlvariant**|O valor definido para esta opção de configuração para as réplicas secundárias.|
|**is_value_default**|**bit** |Especifica se o valor definido é o valor padrão.|
|**dw_compatibility_level**|**int**|O nível de compatibilidade (versão prévia) do banco de dados.  Padrão = 0 (automático)|

## <a name="permissions"></a><a name="Permissions"></a> Permissões

Requer associação à função **pública** .

## <a name="remarks"></a>Comentários

Quando NULL é retornado como o valor para **value_for_secondary**, isso significa que o secundário está definido como PRIMARY.
 
As definições de configurações no escopo do banco de dados serão transferidas para o banco de dados. Isso significa que quando um determinado banco de dados é restaurado ou anexado, as definições de configuração existentes permanecem.

## <a name="see-also"></a>Consulte Também

[ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)
