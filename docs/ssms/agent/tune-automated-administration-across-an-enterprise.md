---
title: Ajustar a administração automatizada em toda a empresa
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 61250c47dd820455f28fec520ecc8224923cc716
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75257864"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>Ajustar a administração automatizada em toda a empresa

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

A administração multisservidor com o Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent se beneficia dos recursos de autoajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Portanto, sob condições normais, não são necessários ajustes adicionais de trabalhos. No entanto, a carga da rede aumenta quando há execução de trabalhos, geração de alertas e notificação de operadores. Você pode ajustar a administração automatizada em toda a empresa para minimizar o tráfego de rede causado por essas atividades.  

## <a name="see-also"></a>Consulte Também

[Monitorando o desempenho do mecanismo de fluxo de dados](../../integration-services/performance/performance-counters.md)