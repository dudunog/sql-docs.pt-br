---
description: sp_control_plan_guide (Transact-SQL)
title: sp_control_plan_guide (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_control_plan_guide
- sp_control_plan_guide_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_plan_guide
ms.assetid: c96d43d5-6507-4d66-b3f5-f44c0617cb5c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b05a3b807f80bccb0c07d876cbb2c10db43f3111
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489503"
---
# <a name="sp_control_plan_guide-transact-sql"></a>sp_control_plan_guide (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Descarta, habilita ou desabilita um guia de plano.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_control_plan_guide [ @operation = ] N'<control_option>'  
  [ , [ @name = ] N'plan_guide_name' ]  
  
<control_option>::=  
{   
    DROP   
  | DROP ALL  
  | DISABLE  
  | DISABLE ALL  
  | ENABLE   
  | ENABLE ALL  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 **N '** _plan_guide_name_ **'**  
 Especifica o guia de plano que está descartado, habilitado ou desabilitado. *plan_guide_name* é resolvido para o banco de dados atual. Se não for especificado, *plan_guide_name* o padrão será NULL.  
  
 DROP  
 Descarta o guia de plano especificado por *plan_guide_name*. Após um guia de plano ser descartado, as execuções futuras de uma consulta anteriormente equivalente ao guia de plano não serão influenciadas pelo guia de plano.  
  
 DROP ALL  
 Descarta todos os guias de plano no banco de dados atual. **N '**_plan_guide_name_ não pode ser especificado quando Remove All é especificado.  
  
 DISABLE  
 Desabilita o guia de plano especificado por *plan_guide_name*. Após um guia de plano ser desabilitado, as execuções futuras de uma consulta anteriormente equivalente ao guia de plano não serão influenciadas pelo guia de plano.  
  
 DISABLE ALL  
 Desabilita todos os guias de plano no banco de dados atual. **N '**_plan_guide_name_ não pode ser especificado quando Disable All é especificado.  
  
 ENABLE  
 Habilita o guia de plano especificado por *plan_guide_name*. Um guia de plano pode ser vinculado a uma consulta elegível após ser habilitado. Por padrão, os guias de plano são habilitados no momento de sua criação.  
  
 ENABLE ALL  
 Habilita todos os guias de plano no banco de dados atual. **N '**_plan_guide_name_**'** não pode ser especificado quando a habilitação All é especificada.  
  
## <a name="remarks"></a>Comentários  
 A tentativa de cancelar ou modificar uma função, procedimento armazenado ou gatilho DML referenciado por um guia de plano, habilitado ou desabilitado, provoca um erro.  
  
 A desabilitação de um guia de plano desabilitado ou a habilitação de um guia de plano habilitado não tem nenhum efeito e ocorre sem erro.  
  
 Os guias de planos não estão disponíveis em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Edições e recursos com suporte no SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md). No entanto, você pode executar **sp_control_plan_guide** com a opção remover ou descartar tudo em qualquer edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="permissions"></a>Permissões  
 Para executar **sp_control_plan_guide** em um guia de plano do tipo objeto (criado especificando ** @type = '** Object **'** ) exige a permissão ALTER no objeto referenciado pelo guia de plano. Todos os outros guias de plano requerem permissão ALTER DATABASE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-enabling-disabling-and-dropping-a-plan-guide"></a>a. Habilitando, desabilitando e descartando um guia de plano  
 O exemplo seguinte cria um guia de plano, desabilita-o, habilita-o e o descarta.  
  
```  
--Create a procedure on which to define the plan guide.  
IF OBJECT_ID(N'Sales.GetSalesOrderByCountry', N'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetSalesOrderByCountry;  
GO  
CREATE PROCEDURE Sales.GetSalesOrderByCountry   
    (@Country nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country;  
END  
GO  
--Create the plan guide.  
EXEC sp_create_plan_guide N'Guide3',  
    N'SELECT *  
    FROM Sales.SalesOrderHeader AS h   
    INNER JOIN Sales.Customer AS c ON h.CustomerID = c.CustomerID  
    INNER JOIN Sales.SalesTerritory AS t ON c.TerritoryID = t.TerritoryID  
    WHERE t.CountryRegionCode = @Country',  
    N'OBJECT',  
    N'Sales.GetSalesOrderByCountry',  
    NULL,  
    N'OPTION (OPTIMIZE FOR (@Country = N''US''))';  
GO  
--Disable the plan guide.  
EXEC sp_control_plan_guide N'DISABLE', N'Guide3';  
GO  
--Enable the plan guide.  
EXEC sp_control_plan_guide N'ENABLE', N'Guide3';  
GO  
--Drop the plan guide.  
EXEC sp_control_plan_guide N'DROP', N'Guide3';  
```  
  
### <a name="b-disabling-all-plan-guides-in-the-current-database"></a>B. Desabilitando todos os guias de plano no banco de dados atual  
 O exemplo seguinte desabilita todos os guias de plano no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_control_plan_guide N'DISABLE ALL';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)   
 [sys.plan_guides &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-plan-guides-transact-sql.md)   
 [Guias de plano](../../relational-databases/performance/plan-guides.md)  
  
  
