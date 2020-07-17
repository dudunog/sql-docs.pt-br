---
title: Conectar a um Utilitário do SQL Server
description: Saiba como se conectar a um Utilitário do SQL Server para que você possa gerenciar a integridade de recursos do SQL Server. É possível conectar-se por meio do SSMS (SQL Server Management Studio).
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fb961ccd1a1ec3013e186c7b45a54004ff400e07
ms.sourcegitcommit: e08d28530e0ee93c78a4eaaee8800fd687babfcc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86301785"
---
# <a name="connect-to-a-sql-server-utility"></a>Conectar a um Utilitário do SQL Server

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Para que você possa se conectar a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é necessário criar um UCP (ponto de controle do utilitário). Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  

Para exibir e gerenciar a integridade de recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) para conectar-se a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  

Para conectar-se a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do SSMS:  

1. Inicie o SSMS.

2. No SSMS, conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

3. Selecione **Exibir** e depois **Gerenciador do Utilitário**.

4. No painel de navegação do Gerenciador do Utilitário, selecione :::image type="icon" source="media/connect-to-utility.gif" border="false"::: **Conectar ao Utilitário**.

5. Na caixa de diálogo **Conectar ao Servidor**, especifique o nome da instância UCP e depois selecione **Conectar**.

6. Exiba o painel de navegação do Gerenciador do Utilitário para ver um modo de exibição de árvore dos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no UCP.

Criar um novo UCP também conecta ao Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Criar um ponto de controle do Utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md).

## <a name="see-also"></a>Consulte Também

- [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)
- [Exibir resultados da política de integridade de recursos &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/view-resource-health-policy-results-sql-server-utility.md)