---
title: 'Propriedades da etapa de trabalho: nova etapa de trabalho (página avançado) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.stepadvanced.f1
ms.assetid: bdecfd4f-bcd8-4ba2-8ada-fbb636314f40
author: stevestein
ms.author: sstein
ms.openlocfilehash: 22b5877fb70a66fd9864e52223b30eca4b01b6db
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064476"
---
# <a name="job-step-properties-new-job-step-advanced-page"></a>Propriedades da Etapa de Trabalho: Nova Etapa de Trabalho (página Avançado)
  Use esta página para exibir e alterar as propriedades de uma [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] etapa de trabalho do Agent.  
  
## <a name="options"></a>Opções  
 **Ação ao obter êxito**  
 Define a ação que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executará se a etapa de trabalho obtiver êxito.  
  
 **Tentativas de repetição**  
 Define o número de vezes que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent tentará repetir uma etapa de trabalho que apresentou falha.  
  
 **Intervalo de repetição (minutos)**  
 Define o tempo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esperará entre as tentativas de repetição.  
  
 **Ação ao falhar**  
 Define a ação que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executará se a etapa de trabalho apresentar falha.  
  
## <a name="options-for-transact-sql-job-steps"></a>Opções para etapas de trabalho Transact-SQL  
 **Arquivo de saída**  
 Define o arquivo a usar para saída da etapa de trabalho. Essa opção só está disponível para os membros da função de servidor fixa **sysadmin** .  
  
 **...**  
 Procura o arquivo a usar para saída da etapa de trabalho.  
  
 **Exibir**  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , esse botão é desabilitado para exibir arquivos de saída. Em vez disso, use o Bloco de Notas para exibir arquivos de saída de etapa de trabalho.  
  
 **Anexar saída ao arquivo existente**  
 Anexa a saída aos conteúdos existentes no arquivo. Caso contrário, os conteúdos anteriores do arquivo serão substituídos a cada vez que a etapa de trabalho for executada.  
  
 **Registrar na tabela**  
 Registra a saída da etapa de trabalho na tabela **sysjobstepslogs** no banco de dados **msdb** .  
  
 **Exibir**  
 Depois de a etapa de trabalho ter sido executada pelo menos uma vez, clique em **Exibir** para exibir sua saída na tabela.  
  
 **Anexar saída à entrada existente na tabela**  
 Anexa a saída aos conteúdos existentes na tabela. Caso contrário, os conteúdos anteriores da tabela serão substituídos a cada vez que a etapa de trabalho for executada.  
  
 **Incluir saída da etapa no histórico**  
 Selecione esta opção para incluir a saída da etapa de trabalho no histórico de trabalho.  
  
 **Executar como usuário**  
 Se você for um membro da função de servidor fixa **sysadmin** , poderá selecionar outro logon do SQL para executar essa etapa de trabalho.  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>Opções para etapas de trabalho do sistema operacional (CmdExec)  
 **Arquivo de saída**  
 Define o arquivo a usar para saída da etapa de trabalho.  
  
 **...**  
 Procura o arquivo a usar para saída da etapa de trabalho.  
  
 **Exibir**  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , esse botão é desabilitado para exibir arquivos de saída. Em vez disso, use o Bloco de Notas para exibir arquivos de saída de etapa de trabalho.  
  
 **Anexar saída ao arquivo existente**  
 Anexa a saída da etapa de trabalho aos conteúdos anteriores do arquivo a cada vez que é executada.  
  
 **Registrar na tabela**  
 Registra a saída da etapa de trabalho na tabela **sysjobstepslogs** no banco de dados **msdb** .  
  
 **Exibir**  
 Depois de a etapa de trabalho ter sido executada pelo menos uma vez, clique em **Exibir** para exibir sua saída na tabela.  
  
 **Anexar saída à entrada existente na tabela**  
 Anexa a saída aos conteúdos existentes na tabela. Caso contrário, os conteúdos anteriores da tabela serão substituídos a cada vez que a etapa de trabalho for executada.  
  
 **Incluir saída da etapa no histórico**  
 Selecione esta opção para incluir a saída da etapa de trabalho no histórico de trabalho.  
  
## <a name="options-for-powershell-job-steps"></a>Opções para etapas de trabalho do PowerShell  
 **Arquivo de saída**  
 Define o arquivo a usar para saída da etapa de trabalho.  
  
 **...**  
 Procura o arquivo a usar para saída da etapa de trabalho.  
  
 **Exibir**  
 No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , esse botão é desabilitado para exibir arquivos de saída. Em vez disso, use o Bloco de Notas para exibir arquivos de saída de etapa de trabalho.  
  
 **Anexar saída ao arquivo existente**  
 Anexa a saída da etapa de trabalho aos conteúdos anteriores do arquivo a cada vez que é executada.  
  
 **Registrar na tabela**  
 Registra a saída da etapa de trabalho na tabela **sysjobstepslogs** no banco de dados **msdb** .  
  
 **Exibir**  
 Depois de a etapa de trabalho ter sido executada pelo menos uma vez, clique em **Exibir** para exibir sua saída na tabela.  
  
 **Anexar saída à entrada existente na tabela**  
 Anexa a saída aos conteúdos existentes na tabela. Caso contrário, os conteúdos anteriores da tabela serão substituídos a cada vez que a etapa de trabalho for executada.  
  
 **Incluir saída da etapa no histórico**  
 Selecione esta opção para incluir a saída da etapa de trabalho no histórico de trabalho.  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>Opções para etapas de trabalho do Replication Queue Reader  
 **Servidor**  
 Define o servidor a usar para uma etapa de trabalho do Replication Queue Reader.  
  
 **Backup de banco de dados**  
 Define o banco de dados a usar para uma etapa de trabalho do Replication Queue Reader.  
  
## <a name="options-for-sql-server-analysis-services-job-steps"></a>Opções para etapas de trabalho do SQL Server Analysis Services  
 **Arquivo de saída**  
 Define o arquivo a usar para saída da etapa de trabalho. Essa opção só está disponível para os membros da função de servidor fixa **sysadmin** .  
  
 **...**  
 Procura o arquivo a usar para saída da etapa de trabalho.  
  
 **Exibir**  
 No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], esse botão está desabilitado para exibir os arquivos de saída. Em vez disso, use o Bloco de Notas para exibir arquivos de saída de etapa de trabalho.  
  
 **Anexar saída ao arquivo existente**  
 Anexa a saída aos conteúdos existentes no arquivo. Caso contrário, os conteúdos anteriores do arquivo serão substituídos a cada vez que a etapa de trabalho for executada.  
  
 **Registrar na tabela**  
 Registra a saída da etapa de trabalho na tabela **sysjobstepslogs** no banco de dados **msdb** .  
  
 **Exibir**  
 Depois de a etapa de trabalho ter sido executada pelo menos uma vez, clique em **Exibir** para exibir sua saída na tabela.  
  
 **Anexar saída à entrada existente na tabela**  
 Anexa a saída aos conteúdos existentes na tabela. Caso contrário, os conteúdos anteriores da tabela serão substituídos a cada vez que a etapa de trabalho for executada.  
  
 **Incluir saída da etapa no histórico**  
 Selecione esta opção para incluir a saída da etapa de trabalho no histórico de trabalho.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar etapas de trabalho](manage-job-steps.md)  
  
  
