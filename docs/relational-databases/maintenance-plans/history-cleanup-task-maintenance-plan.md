---
title: Tarefa de limpeza de histórico (plano de manutenção) | Microsoft Docs
description: Saiba como descartar o histórico de backup/restauração, o Histórico de trabalho do SQL Server Agent e o histórico do plano de manutenção do banco de dados msdb usando a Tarefa Limpeza do Histórico.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.historycleanup.f1
helpviewer_keywords:
- History Cleanup Task dialog box
ms.assetid: 66bb6c39-958c-4053-a27f-b1118d2567f5
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
ms.openlocfilehash: a8fecc3eb56a015ac420ca2cd5167098bbce84ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85667061"
---
# <a name="history-cleanup-task-maintenance-plan"></a>Tarefa limpeza de histórico (Plano de manutenção)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use a caixa de diálogo **Tarefa Limpeza de Histórico** para descartar informações antigas de histórico de tabelas no banco de dados msdb. Essa tarefa oferece suporte a exclusão de backup e restauração de histórico, histórico de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e histórico do plano de manutenção.  
  
 Essa instrução usa as instruções **sp_purge_jobhistory** e **sp_delete_backuphistory** .  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Conexão**  
 Selecione a conexão de servidor a ser usada na execução desta tarefa.  
  
 **Novo**  
 Crie uma nova conexão com o servidor para usar ao executar esta tarefa. A caixa de diálogo **Nova Conexão** é descrita mais abaixo neste tópico.  
  
 **Histórico de backup e restauração**  
 A retenção de registros de quando foram criados backups recentes pode ajudar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a criar um plano de recuperação quando você desejar restaurar um banco de dados. O período de retenção deve ser pelo menos a frequência de backups de banco de dados completos.  
  
 **Histórico de trabalho do SQL Server Agent**  
 Esse histórico pode ajudar a solucionar problemas de trabalhos com falha ou a determinar por que ações de banco de dados ocorreram.  
  
 **Histórico do plano de manutenção**  
 Esse histórico pode ajudar a solucionar problemas de trabalhos de plano de manutenção com falha ou a determinar por que ações de banco de dados ocorreram.  
  
 **Remover dados históricos com mais de**  
 Especifique a idade de itens que deseja excluir.  
  
 **Exibir T-SQL**  
 Exiba as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas no servidor para esta tarefa, com base nas opções selecionadas.  
  
> [!NOTE]  
>  Quando o número de objetos afetados é grande, essa exibição pode ser demorada.  
  
## <a name="new-connection-dialog-box"></a>Caixa de diálogo Nova Conexão  
 **Nome da conexão**  
 Digite um nome para a nova conexão.  
  
 **Selecione ou digite um nome de servidor**  
 Selecione um servidor com o qual se conectar ao executar esta tarefa.  
  
 **Atualizar**  
 Atualize a lista de servidores disponíveis.  
  
 **Digite as informações para fazer logon no servidor**  
 Especifica como autenticar no servidor.  
  
 **Use a segurança integrada do Windows**  
 Conecte a uma instância do SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] com Autenticação do Microsoft Windows.  
  
 **Usar nome de usuário e senha específicos**  
 Conecte a uma instância do SQL Server [!INCLUDE[ssDE](../../includes/ssde-md.md)] que usa a Autenticação do SQL Server. Essa opção não está disponível.  
  
 **Nome de usuário**  
 Forneça um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usado na autenticação. Essa opção não está disponível.  
  
 **Senha**  
 Forneça uma senha a ser usada na autenticação. Essa opção não está disponível.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_purge_jobhistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md)   
 [sp_delete_backuphistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-backuphistory-transact-sql.md)  
  
  
