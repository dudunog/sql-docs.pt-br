---
title: Propriedades do alerta – Novo alerta (página Resposta)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.alert.response.f1
ms.assetid: 72daf008-f9ea-4077-b217-5048e7759d3e
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3266ae4e031088a0db6155d5ee20e792b6d9365c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749227"
---
# <a name="alert-properties---new-alert-response-page"></a>Propriedades do alerta – Novo alerta (página Resposta)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta página para especificar um trabalho que você quer executar e para obter uma lista de operadores a serem notificados em resposta a um alerta do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  

## <a name="options"></a>Opções  
**Executar trabalho**  
Habilita as opções **Lista de trabalhos**, **Novo trabalho** e **Exibir trabalho** .  
  
**Novo trabalho**  
Abra a caixa de diálogo **Novo Trabalho** . Esse botão não está disponível quando **Executar trabalho** não está selecionado.  
  
**Exibir trabalho**  
Exiba ou modifique o trabalho selecionado. Essa opção não está disponível quando **Executar trabalho** não está selecionado.  
  
**Notificar operadores**  
Habilita os controles que permitem adicionar, remover ou alterar operadores.  
  
**Lista de operadores**  
Lista os operadores a notificar quando ocorrer um alerta. Para especificar um método de notificação, marque a caixa de seleção **Email**, **Pager**ou **Net send** que é exibida depois do nome do operador. Essa opção não está disponível quando **Notificar operadores** não está selecionado.  
  
**Email**  
Use email para notificar o operador.  
  
**Pager**  
Use o endereço de email do pager para notificar o operador.  
  
**Net send**  
Use **net send** para notificar o operador.  
  
**Novo operador**  
Exibe a caixa de diálogo **Novo Operador** que você pode usar para criar um operador novo.  
  
**Exibir operador**  
Exibe a caixa de diálogo **Propriedades** para o operador selecionado atualmente. Você pode exibir e modificar as propriedades do operador na caixa de diálogo **Propriedades do Operador**.  
  
## <a name="see-also"></a>Consulte Também  
[Alertas](../../ssms/agent/alerts.md)  
[Create an Alert Using Severity Level](../../ssms/agent/create-an-alert-using-severity-level.md)  
[Alertas](../../ssms/agent/alerts.md)  
[Edit an Alert](../../ssms/agent/edit-an-alert.md)  
[Delete an Alert](../../ssms/agent/delete-an-alert.md)  
  
