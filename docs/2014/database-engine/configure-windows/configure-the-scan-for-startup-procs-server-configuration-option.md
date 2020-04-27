---
title: Configurar a opção de configuração de servidor scan for startup procs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- scan for startup procs option
ms.assetid: 6bf9d252-e766-458d-9dcd-23d895f032a2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a1af9aea2b4088c2a8d3753fd55feaa0f43ae6ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62811363"
---
# <a name="configure-the-scan-for-startup-procs-server-configuration-option"></a>Configurar a opção de configuração de servidor scan for startup procs
  Este tópico descreve como configurar a opção de configuração de servidor **scan for startup procs** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Use a opção **scan for startup procs** para examinar a execução automática de procedimentos armazenados no tempo de inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se essa opção for definida como 1, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] examinará e executará todos os procedimentos armazenados executados automaticamente definidos no servidor. O valor padrão de **scan for startup procs** é 0 (não examinar).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção scan for startup procs usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção verificar processos de inicialização](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   O valor desta opção pode ser definido usando **sp_configure**; porém, será definido automaticamente se você usar **sp_procoption**, que é usado para marcar ou desmarcar automaticamente os procedimentos armazenados executados. Quando **sp_procoption** é usado para marcar o primeiro procedimento armazenado como um autoproc, essa opção é automaticamente definida como um valor 1. Quando **sp_procoption** é usado para desmarcar o último procedimento armazenado como um autoproc, essa opção é automaticamente definida como um valor 0. Se você usar **sp_procoption** para marcar e desmarcar autoprocs, e se você sempre desmarcar autoprocs antes de cancelá-los, não haverá necessidade de definir essa opção manualmente.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-scan-for-startup-procs-option"></a>Para configurar a opção scan for startup procs  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  Em **Diversos**, altere a opção **Examinar Procedimentos de Inicialização** para Verdadeiro ou Falso, selecionando o valor desejado na caixa de listagem suspensa.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-scan-for-startup-procs-option"></a>Para configurar a opção scan for startup procs  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para definir o valor da opção `scan for startup procs` como `1`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'scan for startup procs', 1 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
##  <a name="follow-up-after-you-configure-the-scan-for-startup-procs-option"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar a opção verificar processos de inicialização  
 O servidor deve ser reiniciado para que a configuração entre em vigor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [sp_procoption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql)  
  
  
