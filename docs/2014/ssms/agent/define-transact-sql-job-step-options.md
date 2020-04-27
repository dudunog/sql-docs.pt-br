---
title: Definir opções de etapa de trabalho Transact-SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL job step
- job steps [Transact-SQL]
- SQL Server Agent jobs, Transact-SQL step
ms.assetid: b2a47057-f6fb-432b-a7b6-5d61f33a5d9c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 769e4cb9298ce2a92f7200d9e04743d6b16f842d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62523879"
---
# <a name="define-transact-sql-job-step-options"></a>Define Transact-SQL Job Step Options
  Este tópico descreve como definir opções para etapas [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de [!INCLUDE[tsql](../../includes/tsql-md.md)] trabalho do Agent [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o ou SQL Server Management Objects.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para definir opções de etapa de trabalho Transact-SQL, usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-define-transact-sql-job-step-options"></a>Para definir opções de etapa de trabalho Transact-SQL  
  
1.  No **Pesquisador de Objetos**, expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja editar e clique em **Propriedades**.  
  
2.  Clique na página **Etapas** , clique em uma etapa de trabalho e em **Editar**.  
  
3.  Na caixa de diálogo **Propriedades da Etapa de Trabalho** , confirme que o tipo de trabalho é **Script Transact-SQL (TSQL)** e selecione a página **Avançado** .  
  
4.  Especifique uma ação a tomar em caso de êxito do trabalho, dentre as opções da lista **Ação ao obter êxito** .  
  
5.  Especifique um número de tentativas, inserindo um número entre 0 e 9999 na caixa **Tentativas de repetição** .  
  
6.  Especifique um intervalo entre as tentativas, inserindo um número de minutos entre 0 e 9999 na caixa **Intervalo de repetição** .  
  
7.  Especifique uma ação a tomar em caso de falha do trabalho, dentre as opções da lista **Ação ao falhar** .  
  
8.  Se o trabalho for um script [!INCLUDE[tsql](../../includes/tsql-md.md)] , você poderá escolher entre as seguintes opções:  
  
    -   Inserir o nome de um **Arquivo de saída**. Por padrão, o arquivo é substituído sempre que a etapa de trabalho é executada. Se não quiser que o arquivo de saída seja substituído, marque **Anexar saída ao arquivo existente**. Essa opção só está disponível para membros da função de servidor fixa **sysadmin** . Observe que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] não permite aos usuários visualizar arquivos arbitrários no sistema de arquivos e, portanto, não é possível usar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para exibir logs de etapas de trabalho que são gravados no sistema de arquivos.  
  
    -   Marque **Registrar na tabela** , se desejar registrar a etapa de trabalho em uma tabela de banco de dados. Por padrão, o conteúdo da tabela é substituído sempre que a etapa de trabalho é executada. Se não quiser que o conteúdo da tabela seja substituído, marque **Anexar saída à entrada existente na tabela**. Após a execução da etapa de trabalho, o conteúdo dessa tabela pode ser visualizado clicando-se em **Exibir**.  
  
    -   Marque **Incluir saída da etapa no histórico** , se desejar que a saída seja incluída no histórico da etapa. A saída será exibida apenas se não houver erros. A saída também pode ser truncada.  
  
9. Se você for membro da função de servidor fixa **sysadmin** e desejar executar a etapa de trabalho como um logon SQL diferente, selecione esse logon na lista **Executar como usuário** .  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando SQL Server Management Objects  
 **Para definir opções de etapa de trabalho Transact-SQL**  
  
 Use a classe `JobStep` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell.  
  
  
