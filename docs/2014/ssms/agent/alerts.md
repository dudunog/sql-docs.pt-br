---
title: Alertas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, event types
- SQL Server Agent alerts, names
- alerts [SQL Server], performance conditions
- alerts [SQL Server], about alerts
- WMI event responses [SQL Server Agent alerts]
- events [WMI]
- performance condition alerts [SQL Server Agent]
- alerts [SQL Server], event types
- SQL Server Agent alerts, performance conditions
- SQL Server Agent alerts, about alerts
- alerts [SQL Server], names
ms.assetid: 3f57d0f0-4781-46ec-82cd-b751dc5affef
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b385e6b02807ed79e2becb127a16e76d04329764
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62473127"
---
# <a name="alerts"></a>Alertas
  Eventos são gerados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e inseridos no log de aplicativos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent lê o log de aplicativos e compara os eventos gravados ali com os alertas que você definiu. Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent encontra uma correspondência, ele dispara um alerta, que é uma resposta automatizada a um evento. Além de monitorar eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent também pode monitorar condições de desempenho e eventos do Windows Management Instrumentation (WMI).  
  
 Para definir um alerta, especifique:  
  
-   O nome do alerta.  
  
-   O evento ou condição de desempenho que aciona o alerta.  
  
-   A ação a ser tomada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em resposta ao evento ou condição de desempenho.  
  
## <a name="naming-an-alert"></a>Nomeando um alerta  
 Todo alerta deve ter um nome. Os nomes de alerta devem ser exclusivos dentro da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não podem ultrapassar **128** caracteres.  
  
## <a name="selecting-an-event-type"></a>Selecionando um tipo de evento  
 Um alerta responde a um evento de tipo específico. Alertas respondem aos seguintes tipos de evento:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eventos  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] condições de desempenho  
  
-   Eventos do WMI  
  
 O tipo do evento determina os parâmetros utilizados para especificar o evento preciso.  
  
## <a name="specifying-a-sql-server-event"></a>Especificando um evento do SQL Server  
 É possível especificar que um alerta ocorra em resposta a um ou mais eventos. Use os seguintes parâmetros para especificar os eventos que acionam um alerta:  
  
-   **Número do erro**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent dispara um alerta quando ocorre um erro específico. Por exemplo, você pode especificar o número de erro 2571 como resposta a tentativas não autorizadas de invocar DBCC (Database Console Commands).  
  
-   **Nível de severidade**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent dispara um alerta quando ocorre qualquer erro de uma severidade específica. Por exemplo, você pode especificar um nível de severidade 15 como resposta a erros de sintaxe em instruções Transact-SQL.  
  
-   **Backup de banco de dados**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent só dispara um alerta quando o evento ocorre em um banco de dados específico. Esta opção pode ser aplicada em conjunto com o número de erro ou o nível de severidade. Por exemplo, se uma instância contiver um banco de dados utilizado para produção e outro utilizado para relatórios, você poderá definir um alerta como resposta a erros de sintaxe apenas do banco de dados de produção.  
  
-   **Texto do evento**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent dispara um alerta quando o evento especificado contém uma determinada cadeia de caracteres de texto em sua mensagem. Por exemplo, você pode definir um alerta como resposta a mensagens contendo o nome de uma tabela ou restrição em particular.  
  
## <a name="selecting-a-performance-condition"></a>Selecionando uma condição de desempenho  
 É possível especificar que um alerta ocorra em resposta a uma condição de desempenho em particular. Neste caso, especifique o contador de desempenho a monitorar, o limite do alerta e o comportamento que o contador deve ter face ao alerta. Para definir uma condição de desempenho, é necessário definir os seguintes itens na página [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Geral **da caixa de diálogo** Novo Alerta **ou** Propriedades do Alerta **do** Agent:  
  
-   **Objeto**  
  
     O objeto é a área de desempenho a ser monitorada.  
  
-   **Contador**  
  
     Um contador é um atributo da área a ser monitorada.  
  
-   **Instância**  
  
     A instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define a instância específica (se houver) do atributo a ser monitorado.  
  
-   **Alertar se o contador** e **Valor**  
  
     O limite do alerta e o comportamento que o alerta produz. O limite é um número. O comportamento é um **dos seguintes: cai abaixo**, **torna-se igual a**ou **sobe acima de um número especificado como Valor**. O **Valor** é um número que descreve o contador de condição de desempenho. Por exemplo, para definir que ocorra um alerta para o objeto de desempenho **SQLServer:Locks** quando **Tempo de Espera de Bloqueio** exceder 30 minutos, você deve escolher **sobe acima** e **especificar 30 como valor**.  
  
     Outro exemplo: você pode especificar que ocorra um alerta para o objeto de desempenho **SQLServer:Transactions** quando o espaço livre em **tempdb** cair abaixo de 1000 KB. Para definir isso, bastaria escolher o contador **Espaço livre em tempdb (KB)**, **cai abaixo**e um **Valor** de **1000**.  
  
    > [!NOTE]  
    >  Os dados de desempenho são amostrados periodicamente, o que pode levar a uma pequena demora (alguns segundos) entre o limite a ser atingido e a ocorrência do alerta de desempenho.  
  
## <a name="selecting-a-wmi-event"></a>Selecionando um evento do WMI  
 É possível especificar que um alerta ocorra em resposta a um evento do WMI em particular. Para selecionar um evento WMI, é necessário definir os seguintes itens na página [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Geral **da caixa de diálogo** Novo Alerta **ou** Propriedades do Alerta **do** Agent:  
  
-   **Namespace**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent se registra como um cliente do WMI no namespace do WMI que é fornecido para consulta de eventos.  
  
-   **Consulta**  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent usa a instrução WQL da Instrumentação de Gerenciamento do Windows fornecida para identificar o evento específico.  
  
 Encontram-se, a seguir, os links para tarefas comuns:  
  
 **Para criar um alerta com base em um número de mensagem**  
  
-   [SQL Server Management Studio](create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para criar um alerta com base em níveis de severidade**  
  
-   [SQL Server Management Studio](create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para criar um alerta com base em um evento do WMI**  
  
-   [SQL Server Management Studio](create-a-wmi-event-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Para definir uma resposta a um alerta**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
 **Para criar uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)  
  
 **Para modificar uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
 **Para excluir uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-dropmessage-transact-sql)  
  
 **Para desabilitar ou reativar um alerta**  
  
-   [SQL Server Management Studio](disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
## <a name="see-also"></a>Consulte Também  
 [Usar objetos do SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md)  
  
  
