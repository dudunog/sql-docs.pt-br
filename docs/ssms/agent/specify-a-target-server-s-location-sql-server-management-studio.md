---
description: Especificar a localização de um servidor de destino
title: Especificar a localização de um servidor de destino
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], location
ms.assetid: 511ff311-21f5-4f2f-839f-b4deee26ec98
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 3e09fbc094ddf75a56b2b4c48eac4ecb23b47b7e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482159"
---
# <a name="specify-a-target-server39s-location"></a>Especificar a localização de um servidor de destino
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Este tópico descreve como especificar o local de um servidor de destino em uma configuração de administração multisservidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e Restrições  
Executar essa ação edita o registro. A edição manual do registro não é recomendada, pois alterações incorretas ou não apropriadas podem causar sérios problemas de configuração para o sistema. Portanto, apenas usuários experientes deveriam usar o programa Editor do Registro para editar o registro. Para obter mais informações, consulte a documentação do Microsoft Windows.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-specify-a-target-servers-location"></a>Para especificar o local de um servidor de destino  
  
1.  No **Pesquisador de Objetos,** clique no sinal de adição para expandir o servidor mestre no qual você deseja especificar o local de um servidor de destino.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor** e selecione **Gerenciar Servidores de Destino**.  
  
3.  Clique com o botão direito do mouse em um servidor de destino e selecione **Propriedades**.  
  
4.  Na caixa **Local** , insira um local para o servidor e clique em **OK**.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-specify-a-target-servers-location"></a>Para especificar o local de um servidor de destino  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE msdb ;  
    GO  
    -- enlists the current server into the AdventureWorks1 master server.   
    -- The location for the current server is Building 21, Room 309, Rack 5  
    EXEC dbo.sp_msx_enlist N'AdventureWorks2012',   
        N'Building 21, Room 309, Rack 5' ;  
    GO  
    ```  
  
Para obter mais informações, veja [sp_msx_enlist (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql.md).  
