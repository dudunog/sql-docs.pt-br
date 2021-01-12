---
description: sys.sysobjects (Transact-SQL)
title: Objetos de sys.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sysobjects_TSQL
- sysobjects
- sysobjects_TSQL
- sys.sysobjects
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysobjects compatibility view
- sysobjects system table
ms.assetid: 44fdc387-67b0-4139-8bf5-ed26cf640cd1
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 30d2b16bb9e0366752418fb3e958cdc0600db14b
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98099077"
---
# <a name="syssysobjects-transact-sql"></a>sys.sysobjects (Transact-SQL)
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Contém uma linha para cada objeto criado em um banco de dados, como uma restrição, padrão, log, regra e procedimento armazenado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|name|**sysname**|Nome do objeto|  
|id|**int**|Número de identificação do objeto|  
|xtype|**char(2)**|Tipo de objeto. Pode ser um dos seguintes tipos de objeto:<br /><br /> AF = Função de agregação (CLR)<br /><br /> C = Restrição CHECK<br /><br /> D = Padrão ou restrição DEFAULT<br /><br /> F = Restrição FOREIGN KEY<br /><br /> L = Log<br /><br /> FN = Função escalar<br /><br /> FS = Função escalar de assembly (CLR)<br /><br /> FT = Função avaliada por tabela de assembly (CLR)<br /><br /> IF = Função de tabela em linha<br /><br /> TI = tabela interna<br /><br /> P = Procedimento armazenado<br /><br /> PC = assembly (CLR) armazenado-procedimento<br /><br /> PK = Restrição PRIMARY KEY (o tipo é K)<br /><br /> RF = Procedimento armazenado de filtro de replicação<br /><br /> S = Tabela do sistema<br /><br /> SN = Sinônimo<br /><br /> SQ = Fila de serviço<br /><br /> TA = Gatilho DML de assembly (CLR)<br /><br /> TF = Função de tabela<br /><br /> TR = gatilho DML do SQL<br /><br /> TT = Tipo de tabela<br /><br /> U = Tabela de usuário<br /><br /> UQ = Restrição UNIQUE (o tipo é K)<br /><br /> V = Exibição<br /><br /> X = Procedimento armazenado estendido|  
|uid|**smallint**|ID de esquema do proprietário do objeto. Em bancos de dados atualizados de uma versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o ID de esquema é idêntico ao ID de usuário do proprietário. Excederá ou retornará NULL se o número de usuários e funções exceder 32.767.<br /><br /> Importante se você usar qualquer uma das instruções DDL a seguir, deverá usar a exibição de catálogo **\* Sys. Objects em vez de sys.sysobjetos. \* \* \*** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)<br /><br /> CRIAR &#124; ALTER &#124; DROP USER<br /><br /> CRIAR &#124; ALTERAR &#124; REMOVER FUNÇÃO<br /><br /> CRIAR &#124; ALTERAR &#124; REMOVER FUNÇÃO DE APLICATIVO<br /><br /> CREATE SCHEMA<br /><br /> ALTER AUTHORIZATION ON OBJECT|  
|informações|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|status|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|base_schema_ver|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|replinfo|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|parent_obj|**int**|Número de identificação do objeto pai. Por exemplo, o ID de tabela, se for um gatilho ou restrição.|  
|crdate|**datetime**|A data em que o objeto foi criado.|  
|ftcatid|**smallint**|Identificador do catálogo de texto completo de todas as tabelas de usuário registradas por indexação de texto completo e 0 para todas as tabelas de usuário não registradas.|  
|schema_ver|**int**|Número de versão incrementado toda vez que o esquema de uma tabela muda. Sempre retorna 0.|  
|stats_schema_ver|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|type|**char(2)**|Tipo de objeto. Pode ser um dos seguintes valores:<br /><br /> AF = Função de agregação (CLR)<br /><br /> C = Restrição CHECK<br /><br /> D = Padrão ou restrição DEFAULT<br /><br /> F = Restrição FOREIGN KEY<br /><br /> FN = Função escalar<br /><br /> FS = Função escalar de assembly (CLR)<br /><br /> FT = Função com valor de tabela de assembly (CLR)IF =Função de tabela embutida<br /><br /> IT = Tabela interna<br /><br /> K = Restrição PRIMARY KEY ou UNIQUE<br /><br /> L = Log<br /><br /> P = Procedimento armazenado<br /><br /> PC = assembly (CLR) armazenado-procedimento<br /><br /> R = Regra<br /><br /> RF = Procedimento armazenado de filtro de replicação<br /><br /> S = Tabela do sistema<br /><br /> SN = Sinônimo<br /><br /> SQ = Fila de serviço<br /><br /> TA = Gatilho DML de assembly (CLR)<br /><br /> TF = Função de tabela<br /><br /> TR = gatilho DML do SQL<br /><br /> TT = Tipo de tabela<br /><br /> U = Tabela de usuário<br /><br /> V = Exibição<br /><br /> X = Procedimento armazenado estendido|  
|userstat|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|sysstat|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|indexdel|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|refdate|**datetime**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|version|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|deltrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|instrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|updtrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|seltrig|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|category|**int**|Usado para publicação, restrições e identidade.|  
|cache|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
