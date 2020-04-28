---
title: Conectar a um Utilitário do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: b9b90b8d-241f-4b74-ac14-de7b10ea1821
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9b1b61c1f600667b60601d91a97a1327797daa7b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175885"
---
# <a name="connect-to-a-sql-server-utility"></a>Conectar a um Utilitário do SQL Server
  Para que você possa se conectar a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é necessário criar um UCP (ponto de controle do utilitário). Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](sql-server-utility-features-and-tasks.md).

 Para exibir e gerenciar a integridade de recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS) para conectar-se a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

 Para conectar-se a um Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio do SSMS:

1.  Inicie o SSMS.

2.  No SSMS, conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

3.  Clique em **Exibir** e em **Gerenciador do Utilitário**.

4.  No painel de navegação do Gerenciador do Utilitário, clique em ![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")**Conectar ao Utilitário**.

5.  Na caixa de diálogo **Conectar ao Servidor** , especifique o nome da instância UCP e depois clique em **Conectar**.

6.  Exiba o painel de navegação do Gerenciador do Utilitário para ver um modo de exibição de árvore dos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no UCP.

 Criar um novo UCP também conecta ao Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Criar um ponto de controle do Utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](create-a-sql-server-utility-control-point-sql-server-utility.md).

## <a name="see-also"></a>Consulte Também
 [Utilitário do SQL Server recursos e tarefas](sql-server-utility-features-and-tasks.md) [Exibir Resource Health resultados da política &#40;utilitário do SQL Server&#41;](view-resource-health-policy-results-sql-server-utility.md)


