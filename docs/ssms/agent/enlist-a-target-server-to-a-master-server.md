---
title: Inscrever um servidor de destino em um servidor mestre
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 936c40de1bebd463ad0213ebdfc99171a0fd91a2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75242387"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>Inscrever um servidor de destino em um servidor mestre
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Este tópico descreve como adicionar servidores de destino a uma configuração de administração multisservidor. Execute este procedimento a partir do servidor mestre. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o SMO (SQL Server Management Objects).  
  
Para obter informações sobre como a conta do Windows usada para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent afeta um ambiente multisservidor, consulte [Criar um ambiente multisservidor](../../ssms/agent/create-a-multiserver-environment.md).  
  
Criptografia SSL completa e validação de certificado encontram-se habilitadas, por padrão, para conexões entre servidores mestre e servidores de destino. Para obter mais informações, veja [Definir opções de criptografia em servidores de destino](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-enlist-a-target-server"></a>Para inscrever um servidor de destino  
  
1.  No **Pesquisador de Objetos**, expanda um servidor que esteja configurado como servidor mestre.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Adicionar Servidores de Destino**.  
  
3.  Complete o Assistente de Servidor de Destino, que o guia nesse processo.  
  
## <a name="using-transact-sql"></a><a name="TsqlProcedure"></a>Usando Transact-SQL  
  
#### <a name="to-enlist-a-target-server"></a>Para inscrever um servidor de destino  
  
1.  Use o procedimento armazenado **sp_msx_enlist** .  Para obter mais informações, veja [sp_msx_enlist (Transact-SQL)](https://msdn.microsoft.com/ceb3b2bc-0cc4-48d8-9bdc-6a809556e35f)  
  
## <a name="see-also"></a>Consulte Também  
[Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
