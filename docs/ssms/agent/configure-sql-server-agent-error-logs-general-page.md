---
title: Configurar logs de erros (página Geral)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.configure.f1
ms.assetid: e08de622-6f87-470c-aee0-b2d6cb6cca88
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 1f5c804350a71ae4834a1bbc689a2bc3d6fbc73c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246078"
---
# <a name="configure-sql-server-agent-error-logs-general-page"></a>Configurar Logs de Erros do SQL Server Agent (página Geral)

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use esta tela para exibir e atualizar as configurações de log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Arquivo de log de erros**  
Especifica o arquivo em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent grava logs de erros.  
  
**...**  
Navegue até o arquivo de log de erros.  
  
**Gravar log de erros OEM**  
Grava o arquivo de log de erros como um arquivo não Unicode. Isso reduz a quantidade de espaço em disco consumida pelo arquivo de log. Porém, mensagens que incluem dados Unicode podem ser mais difíceis de ler quando essa opção é habilitada.  
  
**Erros**  
Só grava erros e mensagens informativas no arquivo de log.  
  
**Warnings**  
Só grava avisos e mensagens informativas no arquivo de log.  
  
**Informações**  
Só grava mensagens informativas no arquivo de log.  
  
## <a name="see-also"></a>Consulte Também  
[Log de erros do SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
