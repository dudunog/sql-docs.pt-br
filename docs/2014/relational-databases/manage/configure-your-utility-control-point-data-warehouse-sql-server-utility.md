---
title: Configurar seu data warehouse do ponto de controle do utilitário (Utilitário do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: c2c6f050-8cdb-4b8e-ad38-4aae0a949847
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 60b9623b468f2763cf619c325412373e3603f3a3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85023637"
---
# <a name="configure-your-utility-control-point-data-warehouse-sql-server-utility"></a>Configurar o data warehouse a partir do ponto de controle do utilitário (Utilitário do SQL Server)
  Dados coletados por instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são armazenados no UMDW (data warehouse de gerenciamento do utilitário); o nome de arquivo UMDW é sysutility_mdw.  
  
 É possível configurar o período de retenção de dados do UMDW. Para obter mais informações, veja [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md).  
  
 Os parâmetros de configuração a seguir não podem ser configurados nesta versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Nome do UMDW: Sysutility_mdw.  
  
-   Frequência de carregamento do conjunto de coleta: a cada 15 minutos.  
  
 O diretório UMDW é configurável: \<System drive> : \Program Files\Microsoft SQL Server \ MSSQL10_50. <UCP_Name> \MSSQL\Data \\ , onde \<System drive> é normalmente o C:\ Dirigir. O arquivo de log, Sysutility_mdw_ \<GUID> _LOG, está localizado no mesmo diretório.  
  
> [!NOTE]  
>  O local do arquivo UMDW (sysutility_mdw) pode ser alterado usando-se desanexar/anexar ou ALTER DATABASE. É recomendável usar ALTER DATABASE. Para obter mais informações, veja [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos e tarefas do utilitário do SQL Server](sql-server-utility-features-and-tasks.md)  
  
  
