---
description: sys.dm_clr_properties (Transact-SQL)
title: sys.dm_clr_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_properties
- sys.dm_clr_properties_TSQL
- dm_clr_properties_TSQL
- dm_clr_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_properties dynamic management view
ms.assetid: 220d062f-d117-46e7-a448-06fe48db8163
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 34dfbfbecf82df79520fc5a530bcb8c18c544c77
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095259"
---
# <a name="sysdm_clr_properties-transact-sql"></a>sys.dm_clr_properties (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  Retorna uma linha para cada propriedade relacionada à integração common language runtime (CLR) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo a versão e o estado de CLR hospedado. O CLR hospedado é inicializado executando as instruções [Create assembly](../../t-sql/statements/create-assembly-transact-sql.md), [ALTER ASSEMBLY](../../t-sql/statements/alter-assembly-transact-sql.md)ou [drop assembly](../../t-sql/statements/drop-assembly-transact-sql.md) , ou executando qualquer rotina, tipo ou gatilho CLR. A exibição **Sys.dm_clr_properties** não especifica se a execução do código CLR do usuário foi habilitada no servidor. A execução do código CLR do usuário é habilitada usando o procedimento armazenado [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) com a opção [CLR Enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md) definida como 1.  
  
 A exibição **Sys.dm_clr_properties** contém as colunas **nome** e **valor** . Cada linha nesta exibição fornece detalhes sobre uma propriedade do CLR hospedado. Use esta exibição para coletar informações sobre o CLR hospedado, como o diretório de instalação do CLR, a versão do CLR e o estado atual do CLR hospedado. Esta exibição poderá ajudá-lo a determinar se o código de integração CLR não está funcionando devido a problemas com a instalação de CLR no computador do servidor.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|O nome da propriedade.|  
|**value**|**nvarchar(128)**|Valor da propriedade.|  
  
## <a name="properties"></a>Propriedades  
 A propriedade **Directory** indica o diretório no qual o .NET Framework foi instalado no servidor. Pode haver várias instalações do .NET Framework no computador do servidor e o valor dessa propriedade identifica qual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de instalação está sendo usada.  
  
 A propriedade **version** indica a versão do .NET Framework e o CLR hospedado no servidor.  
  
 A exibição gerenciada dinâmica **Sys.dm_clr_properties** pode retornar seis valores diferentes para a propriedade de **estado** , que reflete o estado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CLR hospedado. Elas são:  
  
-   Mscoree não está carregado.  
  
-   Mscoree está carregado.  
  
-   Versão de CLR bloqueada com mscoree.  
  
-   CLR é inicializado.  
  
-   Inicialização de CLR falhou permanentemente.  
  
-   CLR é interrompido.  
  
 O **mscoree não é carregado** e os Estados de **mscoree são carregados** mostram a progressão da inicialização CLR hospedada na inicialização do servidor e provavelmente não serão vistos.  
  
 A **versão do CLR bloqueada com** o estado do mscoree pode ser vista onde o CLR hospedado não está sendo usado e, portanto, ainda não foi inicializado. O CLR hospedado é inicializado na primeira vez que uma instrução DDL (como [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)) ou um objeto de banco de dados gerenciado é executado.  
  
 O estado do **CLR é inicializado** indica que o CLR hospedado foi inicializado com êxito. Observe que isso não indica se a execução do código CLR do usuário foi habilitada. Se a execução do código CLR do usuário for habilitada primeiro e, em seguida, desabilitada usando o [!INCLUDE[tsql](../../includes/tsql-md.md)] procedimento armazenado [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) , o valor do estado ainda será o **CLR inicializado**.  
  
 O estado de **falha de inicialização do CLR permanentemente** indica que a inicialização do CLR hospedado falhou. A pressão de memória é uma causa provável ou também poderia ser o resultado de uma falha no handshake de hospedagem entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o CLR. Nesse caso, será gerada a mensagem de erro 6512 ou 6513.  
  
 O **estado CLR é parado** só é visto quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está no processo de desligamento.  
  
## <a name="remarks"></a>Comentários  
 As propriedades e os valores dessa exibição podem ser alterados em uma versão futura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devido a aprimoramentos da funcionalidade de integração CLR.  
  
## <a name="permissions"></a>Permissões  
  
Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão.   
Nos objetivos do serviço básico, S0 e S1 do banco de dados SQL, e para bancos de dados em pools elásticos, o `Server admin` ou uma `Azure Active Directory admin` conta é necessária. Em todos os outros objetivos de serviço do banco de dados SQL, a `VIEW DATABASE STATE` permissão é necessária no banco de dados.   

## <a name="examples"></a>Exemplos  
 O exemplo a seguir recupera informações sobre o CLR hospedado:  
  
```  
SELECT name, value   
FROM sys.dm_clr_properties;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições e funções de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
