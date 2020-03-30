---
title: Propriedades de conta proxy – Conta proxy nova (página Geral)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.proxy.general.f1
ms.assetid: 5cd81265-bf59-413b-8397-150ddc70d0c7
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 86c381bb502b95fc0875ea45348dc01912ccb64c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75247591"
---
# <a name="proxy-account-properties---new-proxy-account-general-page"></a>Propriedades de conta proxy – Conta proxy nova (página Geral)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa página para exibir ou alterar as propriedades de uma conta proxy do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opções  
**Nome do proxy**  
Digite o nome do proxy.  
  
**Nome da credencial**  
Digite o nome da credencial para o proxy.  
  
> [!NOTE]  
> O nome da credencial fornecido deve ser o nome de uma credencial existente. Para obter informações sobre como criar credenciais, veja [Como Criar um proxy](https://msdn.microsoft.com/c1e77e91-2a69-40d9-b8b3-97cffc710586)  
  
**...**  
Inicia a caixa de diálogo **Selecionar Credencial** .  
  
**Descrição**  
Digite a descrição para o proxy.  
  
**Ativo nos seguintes subsistemas**  
Selecione os subsistemas para os quais a conta proxy tem acesso.  
  
**Reatribuir etapas de trabalho para**  
Selecione o proxy para o qual reatribuir etapas de trabalho. Essa lista está habilitada quando você revogar o acesso a um subsistema para o qual proxy tinha acesso anteriormente.  
  
## <a name="see-also"></a>Consulte Também  
[Criar um proxy do SQL Server Agent](../../ssms/agent/create-a-sql-server-agent-proxy.md)  
  
