---
title: Exibir um log de auditoria do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audits [SQL Server], viewing logs
- viewing audit logs
- logs [SQL Server], audit
ms.assetid: e8feaca0-7852-422b-895a-319b965d8d9b
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8f9902a4fc92ef0b35bae62eb80170762c52fdec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055450"
---
# <a name="view-a-sql-server-audit-log"></a>Exibir um log auditoria do SQL Server
  Este tópico descreve como exibir um log de auditoria do SQL Server no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir um log de auditoria do SQL Server usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão `CONTROL SERVER`.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-a-sql-server-audit-log"></a>Para exibir um log de auditoria do SQL Server  
  
1.  No Pesquisador de Objetos, expanda a pasta **Segurança** .  
  
2.  Expanda a pasta **Auditorias** .  
  
3.  Clique com o botão direito do mouse no log de auditoria que você deseja exibir e selecione **Exibir Logs de Auditoria**. Isso abre a caixa de diálogo **Visualizador do arquivo de log-**_server_name_ . Para obter mais informações, consulte [Log File Viewer F1 Help](../../logs/log-file-viewer-f1-help.md).  
  
4.  Quando terminar, clique em **Fechar**.  
  
 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] recomenda exibir o log de auditoria usando o Visualizador do Arquivo de Log. No entanto, se você estiver criando um sistema de monitoramento automatizado, as informações no arquivo de auditoria podem ser lidas diretamente usando a função [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql). Ler o arquivo diretamente retorna dados em um formato ligeiramente diferente (não processado). Consulte **sys.fn_get_audit_file** para obter mais informações  
  
## <a name="see-also"></a>Consulte Também  
 [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](sql-server-audit-database-engine.md)   
 [Gravar eventos de auditoria do SQL Server no log de segurança](write-sql-server-audit-events-to-the-security-log.md)  
  
  
