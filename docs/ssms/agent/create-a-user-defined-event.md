---
description: Criar um evento definido pelo usuário
title: Criar um evento definido pelo usuário
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fdd45d02833b478b83b3a674c078cb7975a24436
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88371412"
---
# <a name="create-a-user-defined-event"></a>Criar um evento definido pelo usuário
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Você pode criar eventos definidos pelo usuário caso deseje monitorar eventos diferentes daqueles predefinidos pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você também pode atribuir um nível de severidade a cada evento definido pelo usuário.  
  
> [!NOTE]  
> Ao usar o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selecione a opção **Gravar no log de eventos de aplicativo do Windows** para cada mensagem de evento definido pelo usuário, a fim de garantir que as mensagens sejam registradas. Por padrão, as mensagens definidas pelo usuário que tenham severidade abaixo de 19 não são enviadas ao log de aplicativos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows quando ocorrem. Portanto, as mensagens definidas pelo usuário que tenham severidade abaixo de 19 não disparam alertas do SQL Server Agent.  
  
Os eventos definidos pelo usuário devem ter um número de mensagem exclusivo. Os números de mensagem de um evento definido pelo usuário devem ser maiores que 50.000. Você pode definir mensagens para o evento em múltiplos idiomas. No entanto, deve existir uma mensagem de erro em **En-US** para que possam ser adicionadas mensagens em outros idiomas.  
  
Se você administra um ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] multilíngue, crie mensagens definidas pelo usuário em cada um dos idiomas com suporte. Por exemplo, se estiver criando uma nova mensagem de evento a ser usada em dois servidores, um em inglês e outro em alemão, use o mesmo número de mensagem e de severidade para ambos, mas atribua um idioma diferente a cada um.  
  
As seguintes tarefas proporcionam informações sobre como criar eventos definidos pelo usuário e alertas em resposta a eles:  
  
**Para criar um alerta com base em um número de mensagem**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**Para criar um alerta com base em níveis de severidade**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/d9b41853-e22d-4813-a79f-57efb4511f09)  
  
**Para definir uma resposta a um alerta**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/0525e0a2-ed0b-4e69-8a4c-a9e3e3622fbd)  
  
**Para criar uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](https://msdn.microsoft.com/54746d30-f944-40e5-a707-f2d9be0fb9eb)  
  
**Para modificar uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](https://msdn.microsoft.com/1b28f280-8ef9-48e9-bd99-ec14d79abaca)  
  
**Para excluir uma mensagem de erro de evento definida pelo usuário**  
  
-   [Transact-SQL](https://msdn.microsoft.com/17287a15-cdde-43d1-bb18-9f920bc15db8)  
  
**Para desabilitar ou reativar um alerta**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](https://msdn.microsoft.com/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
## <a name="see-also"></a>Consulte Também  
[sp_update_alert (Transact-SQL)](https://msdn.microsoft.com/4bbaeaab-8aca-4c9e-abc1-82ce73090bd3)  
  
