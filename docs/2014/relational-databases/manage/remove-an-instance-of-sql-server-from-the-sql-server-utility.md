---
title: Remover uma instância do SQL Server por meio do Utilitário do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.utility.remove.f1
ms.assetid: ae1d126a-46d2-47bf-b339-17c743df6491
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: df13432a0b5f835690dd6371fd935198d7798b40
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72783287"
---
# <a name="remove-an-instance-of-sql-server-from-the-sql-server-utility"></a>Remover uma instância do SQL Server do Utilitário do SQL Server
  Use as etapas a seguir para remover uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este procedimento remove a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da exibição de lista do UCP e a coleta de dados do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é interrompida. A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é desinstalada.  
  
> [!IMPORTANT]  
>  Antes de realizar este procedimento para remover uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility, tenha certeza de que os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e SQL Server Agent estão sendo executados na instância a ser removida.  
  
1.  No Gerenciador do Utilitário no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique em **Instâncias Gerenciadas**. Observe a exibição de lista das instâncias registradas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no painel de conteúdo do Gerenciador do Utilitário.  
  
2.  Na coluna **Nome de Instância do SQL Server** da exibição de lista, selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser removida do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Clique com o botão direito do mouse na instância a ser removida e selecione **Remover Instância Gerenciada...** .  
  
3.  Especifique as credenciais com privilégios de administrador da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: clique em **Conectar...** , verifique as informações na caixa de diálogo **Conectar ao Servidor** e clique em **Conectar**. Você verá as informações de logon na caixa de diálogo **Remover Instância Gerenciada** .  
  
4.  Para confirmar a operação, clique em **OK**. Para encerrar a operação, clique em **Cancelar**.  
  
## <a name="manually-remove-a-managed-instance-of-sql-server-from-a-sql-server-utility"></a>Remover manualmente uma instância gerenciada do SQL Server do Utilitário do SQL Server  
 Este procedimento remove a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da exibição de lista do UCP e interrompe a coleta de dados do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não é desinstalada.  
  
 Para usar o PowerShell para remover uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esse script executa as seguintes operações:  
  
-   Obtém o UCP pelo nome da instância do servidor.  
  
-   Remove a instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```powershell
# Get Ucp connection  
$UcpServerInstanceName = "ComputerName\InstanceName";  
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $UcpServerInstanceName;  
$UcpConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::Connect($UcpConnection);  
  
# Now remove the ManagedInstance from the SQL Server Utility  
$ServerInstanceName = "ComputerName\InstanceName";  
$Instance = new-object -Type Microsoft.SqlServer.Management.Smo.Server $ServerInstanceName;  
$InstanceConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $Instance.ConnectionContext.SqlConnectionObject;  
$ManagedInstance = $Utility.ManagedInstances[$ServerInstanceName];  
$ManagedInstance.Remove($InstanceConnection);  
```  
  
É importante fazer referência ao nome da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância exatamente como armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em uma instância com diferenciação de maiúsculas e minúsculas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você deve especificar o nome da instância usando exatamente as maiúsculas e minúsculas, conforme retornado por @@SERVERNAME. 

Para obter o nome de instância para a instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], execute esta consulta na instância gerenciada:  
  
```sql
select @@SERVERNAME AS instance_name  
```  
  
 Neste momento, a instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é removida completamente do UCP. Ela desaparece da exibição de lista da próxima vez que você atualizar os dados para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Este estado é idêntico para um usuário que consegue remover uma instância gerenciada na interface de usuário do SSMS.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o Gerenciador do Utilitário para gerenciar o Utilitário do SQL Server](use-utility-explorer-to-manage-the-sql-server-utility.md)   
 [Solucionar problemas do Utilitário do SQL Server](../../database-engine/troubleshoot-the-sql-server-utility.md)  
