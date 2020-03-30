---
title: Administrar vários servidores usando Servidores de Gerenciamento Central
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: a2e2da55bd04ba29cf1c6ef81757488f8d50fd24
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74055615"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>Administrar vários servidores usando Servidores de Gerenciamento Central
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Você pode administrar vários servidores designando servidores de gerenciamento centrais e criando grupos de servidores.  
  
## <a name="what-is-a-central-management-server-and-server-groups"></a>O que é um Servidor de Gerenciamento Central e grupos de servidores?  
 Uma instância do SQL Server, designada como um Servidor de Gerenciamento Central, mantém grupos de servidores que contêm as informações de conexão de uma ou mais instâncias. É possível executar instruções [!INCLUDE[tsql](../includes/tsql-md.md)] e políticas de Gerenciamento Baseado em Políticas ao mesmo tempo nos grupos de servidores. Também é possível exibir os arquivos de log em instâncias gerenciadas por meio de um Servidor de Gerenciamento Central. 
 
 Basicamente, um Servidor de Gerenciamento Central é um repositório central que contém uma lista dos servidores gerenciados. As versões anteriores ao [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] não podem ser designadas como um Servidor de Gerenciamento Central.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] também podem ser executadas nos grupos de servidor locais em Servidores Registrados.  
  
## <a name="create-central-management-server-and-server-groups"></a>Criar um Servidor de Gerenciamento Central e grupos de servidores 
 Para criar um Servidor de Gerenciamento Central e grupos de servidores, use a janela **Servidores Registrados** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Observe que o Servidor Central de Gerenciamento não pode ser membro de um grupo que o mantém. 
 
 Para saber como criar Servidores de Gerenciamento Central e grupos de servidores, consulte [Criar um Servidor de Gerenciamento Central e grupo de servidores &#40;SQL Server Management Studio&#41;](../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  
  
## <a name="see-also"></a>Confira também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
