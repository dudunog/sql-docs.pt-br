---
title: Exibir um log de erros do SQL Server Agent (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- viewing SQL Server Agent error logs
- displaying SQL Server Agent error logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: de920425-fa44-469f-b83d-49e3f97e97f4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3835f83efff9e720f7f8631d527b9547e3b4239a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245606"
---
# <a name="view-sql-server-agent-error-log-sql-server-management-studio"></a>View SQL Server Agent Error Log (SQL Server Management Studio)
  Este tópico descreve como exibir o log de erros do  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 O Visualizador do Arquivo de Log exibe informações de muitos componentes diferentes. Quando o Visualizador do Arquivo de Log estiver aberto, use o painel **Selecionar logs** para selecionar os logs que deseja exibir. Cada log exibe as colunas adequadas àquele tipo de log. Os logs disponíveis dependem de como o Visualizador do Arquivo de Log é aberto.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   [Para exibir o log de erros do SQL Server Agent usando o SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 O Pesquisador de Objetos só exibirá o nó [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se você tiver permissão para usá-lo.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Para executar suas funções, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve ser configurado de modo a usar as credenciais de uma conta que seja membro da função de servidor fixa **sysadmin** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A conta deve ter as seguintes permissões do Windows:  
  
-   Fazer logon como um serviço (SeServiceLogonRight)  
  
-   Substituir um token de nível de processo (SeAssignPrimaryTokenPrivilege)  
  
-   Ignorar verificação completa (SeChangeNotifyPrivilege)  
  
-   Ajustar cotas de memória para um processo (SeIncreaseQuotaPrivilege)  
  
 Para obter mais informações sobre as permissões do Windows necessárias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a conta de serviço do Agent, consulte [selecionar uma conta para o serviço de SQL Server Agent](select-an-account-for-the-sql-server-agent-service.md) e [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-the-ssnoversion-agent-error-log"></a>Para exibir o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que você deseja exibir.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Logs de erro** .  
  
4.  Clique com o botão direito do mouse no log de erros que você deseja exibir e selecione **Exibir Log do Agente**.  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Visualizador do Arquivo de Log -**_nome_do_servidor_:  
  
     **Carregar Log**  
     Abra uma caixa de diálogo onde seja possível especificar um arquivo de log a ser carregado.  
  
     **Exportar**  
     Abra uma caixa de diálogo que permita exportar as informações mostradas na grade **Resumo do arquivo de log** para um arquivo de texto.  
  
     **Atualizar**  
     Atualize a exibição dos logs selecionados. O botão **Atualizar** relê os logs selecionados do servidor de destino ao aplicar qualquer configuração de filtro.  
  
     **Filter**  
     Abra uma caixa de diálogo que permita especificar configurações usadas para filtrar o arquivo de log, como **Conexão**, **Data**ou outros critérios de filtragem **Gerais** .  
  
     **Pesquisa**  
     Pesquise o texto específico no arquivo de log. Não há suporte à pesquisa com caracteres curinga.  
  
     **Parar**  
     Interrompe o carregamento das entradas do arquivo de log. Por exemplo, você poderá usar essa opção se um arquivo de log remoto ou offline demorar muito tempo para ser carregado e você desejar exibir apenas as entradas mais recentes.  
  
     **Resumo do arquivo de log**  
     Esse painel de informações exibe um resumo da filtragem do arquivo de log. Se o arquivo não for filtrado, você verá o seguinte texto, **Nenhum filtro aplicado**. Se um filtro for aplicado ao log, você verá o texto **Filtrar entradas do log, em que: ** \<critérios do filtro>.  
  
     **Detalhes da linha selecionada**  
     Selecione uma linha para exibir detalhes adicionais sobre a linha de evento selecionada na parte inferior da página. As colunas podem ser reordenadas arrastando-as para locais novos na grade. As colunas podem ser redimensionadas arrastando para a esquerda ou direta as barras separadoras de coluna no cabeçalho de grade. Clique duas vezes nas barras separadoras de coluna no cabeçalho da grade para dimensionar automaticamente a coluna para a largura do conteúdo.  
  
     **Instância**  
     O nome da instância do na qual ocorreu o evento. Isso é exibido como nome da*instância*do *nome*\\do computador.  
  
     **Data**  
     Exibe a data do evento.  
  
     **Fonte**  
     Exibe o recurso de origem do qual o evento é criado, como o nome do serviço (MSSQLSERVER, por exemplo). Isso não é exibido para todos os tipos de log.  
  
     **Mensagem**  
     Exibe todas as mensagens associadas ao evento.  
  
     **Tipo de Log**  
     Exibe o tipo de log ao qual o evento pertence. Todos os logs selecionados são exibidos na janela de resumo de arquivo de log.  
  
     **Origem do Log**  
     Exibe uma descrição do log de origem no qual o evento é capturado.  
  
5.  Quando terminar, clique em **Fechar**.  
  
  
