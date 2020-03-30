---
title: Depurar um manipulador de lógica de negócios (programação de replicação)
description: Saiba como usar um manipulador de lógica de negócios para invocar a lógica de negócios personalizada quando uma assinatura de mesclagem for sincronizada.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- merge replication business logic handlers [SQL Server replication]
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: edd0d17a-0e9c-4c28-8395-a7d47e8ce3d6
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b001e9e53c30ba57b2a56b0bd57571668ae2770c
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75321773"
---
# <a name="debug-a-business-logic-handler-replication-programming"></a>Depurar um manipulador de lógica de negócios (Programação de replicação)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use um manipulador de lógica de negócios para invocar a lógica de negócios personalizada quando uma assinatura de mesclagem for sincronizada. Para obter mais informações, consulte [Executar lógica de negócios durante a sincronizações de mesclagem](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 O Reconciliador de replicação de mesclagem (replrec.dll) chama o assembly de código gerenciado que contém a lógica comercial. Na maior parte dos casos, o replrec.dll e a lógica comercial personalizada são executados no computador em que o Agente de Mesclagem é executado (no Assinante para a assinatura pull ou no Distribuidor da assinatura push). Com relação à sincronização da Web ou a um Assinante [!INCLUDE[ssEW](../../includes/ssew-md.md)] , o reconciliador e a lógica comercial personalizada são executados no servidor Web.  
  
### <a name="to-debug-a-business-logic-handler-on-a-local-computer"></a>Para depurar um manipulador de lógica de negócios em um computador local  
  
1.  Configure a publicação e a distribuição, crie uma publicação e crie uma assinatura para a publicação. Para obter mais informações, confira [Configurar publicação e distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md) e [Criar uma publicação](../../relational-databases/replication/publish/create-a-publication.md).  
  
2.  Crie e registre um manipulador de lógica de negócios. Para obter mais informações, consulte [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
3.  Crie um projeto RMO (Replication Management Objects) no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio, que iniciará o Agente de Mesclagem em sincronia, programaticamente. Para obter mais informações, consulte [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md).  
  
4.  Defina um ponto de interrupção no código do manipulador de lógica de negócios, tanto no método sendo depurado como no construtor da classe. Para obter mais informações sobre os métodos que podem ser implementados no manipulador de lógica de negócios, consulte o tópico dos métodos <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> .  
  
5.  Crie o manipulador de lógica de negócios no modo de depuração e implante o assembly e o arquivo de símbolo de depuração (.pdb) no local registrado na Etapa 1.  
  
    > [!NOTE]  
    >  Para simplificar a depuração, crie uma solução única de Visual Studio .NET que contenha ambos o projeto do manipulador de lógica de negócios e o projeto que sincroniza a assinatura. Nesse caso, defina o projeto de sincronização como projeto de inicialização e configure o ambiente de compilação para implantar o assembly da lógica comercial no local registrado na Etapa 1, durante a depuração.  
  
6.  Execute a inserção, atualize ou exclua comandos de acordo com a assinatura ou banco de dados de publicação. O comando e o local da execução dependem do método que é depurado.  
  
7.  Inicie o projeto na Etapa 3, em modo de depuração, para sincronizar a assinatura.  
  
8.  Supondo que nenhum outro ponto de interrupção esteja definido e que os comandos tenham sido replicados, a execução para quando alcança o ponto de interrupção do manipulador de lógica de negócios.  
  
### <a name="to-debug-a-business-logic-handler-on-a-web-server-using-web-synchronization-or-for-a-sql-server-compact-subscriber"></a>Para depurar um manipulador de lógica de negócios em um servidor Web usando a sincronização da Web ou para um assinante do SQL Server Compact  
  
1.  Configure a publicação e a distribuição, crie uma publicação e crie uma assinatura pull para a publicação. A publicação deve oferecer suporte para sincronização da Web ou Assinantes [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
2.  Crie e registre um manipulador de lógica de negócios. Para obter mais informações, consulte [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md).  
  
3.  Defina um ponto de interrupção no código do manipulador de lógica de negócios, tanto no método sendo depurado como no construtor da classe. Para obter mais informações sobre os métodos que podem ser implementados no manipulador de lógica de negócios, consulte o tópico dos métodos <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> .  
  
4.  Crie o manipulador de lógica de negócios no modo de depuração e implante o assembly e o arquivo de símbolo de depuração (.pdb) no local registrado na Etapa 1.  
  
    > [!NOTE]  
    >  Se o manipulador de lógica de negócios falhar em criar por causa do assembly que está em uso, digite o comando `iisreset` no servidor Web, no prompt de comando do servidor Web.  
  
5.  Sincronize a assinatura com sincronização da Web ativada. Durante a sincronização, o servidor Web carrega o assembly registrado.  
  
6.  Usando o depurador do Visual Studio .NET, anexe a um dos processos seguintes no servidor Web:  
  
    -   w3wp.exe - Windows Server 2003.  
  
    -   inetinfo.exe - Windows 2000 e Windows XP.  
  
7.  Na janela de **Saída** , verifique a saída da depuração para confirmar se os símbolos do assembly registrado foram carregados corretamente. Se os símbolos não estiverem carregados, confirme se o arquivo .pdb correto foi copiado na Etapa 4, e repita a Etapa 5.  
  
8.  Execute a inserção, atualize ou exclua comandos de acordo com a assinatura ou banco de dados de publicação. O comando e o local da execução dependem do método que é depurado.  
  
9. Usando o depurador do Visual Studio, anexe ao processo w3wp.exe.  
  
10. Sincronize a assinatura novamente usando a sincronização da Web.  
  
11. Supondo que nenhum outro ponto de interrupção esteja definido e que os comandos tenham sido replicados, a execução para quando alcança o ponto de interrupção do manipulador de lógica de negócios.  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
