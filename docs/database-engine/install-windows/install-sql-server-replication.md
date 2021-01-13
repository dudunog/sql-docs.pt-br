---
title: Instalar a Replicação do SQL Server | Microsoft Docs
description: Instale componentes de replicação usando o Assistente de Instalação do SQL Server ou em uma janela do prompt de comando.
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server replication]
- command line installations [SQL Server replication]
- installing replication
- replication [SQL Server], installing
- command prompt [SQL Server replication]
ms.assetid: c50ad078-060b-4a8d-ad45-9e31a8d85729
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: b1995d22488693a31adb7c9a421f5a2e32de463d
ms.sourcegitcommit: 3ec49252e82590de0fe559a8574606ae213f6f3b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97975436"
---
# <a name="install-sql-server-replication"></a>Instalar a replicação do SQL Server

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

É possível instalar componentes de replicação usando o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou um prompt de comando. Instale a replicação ao instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou ao modificar uma instância existente.  
  
Depois da instalação dos componentes de replicação, é necessário configurar o servidor antes de usar a replicação. Para obter mais informações, veja [Configurar distribuição](../../relational-databases/replication/configure-distribution.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
>[!IMPORTANT]  
>Se você instalar componentes de replicação ao modificar uma instância existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é necessário parar e reiniciar o agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando a instalação for concluída. Essa ação ajuda a assegurar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent reconheça os subsistemas de agente de replicação e possa chamar agentes de replicação em etapas de trabalho.  
  
## <a name="installing-replication-by-using-setup"></a>Instalando a replicação usando a instalação  
**Para instalar a replicação ao instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- Para instalar componentes de replicação, incluindo o RMO (Replication Management Objects), selecione **SQL Server Replication** na página **Seleção de Recursos** do Assistente de Instalação.  
  
## <a name="installing-replication-from-the-command-prompt"></a>Instalando a replicação a partir do prompt de comando  
 **Para instalar a replicação ao instalar uma nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**  
  
- Consulte [Instalar o SQL Server do prompt de comando](./install-sql-server-from-the-command-prompt.md).  
  
## <a name="see-also"></a>Confira também  
 [Instalar o SQL Server](../../database-engine/install-windows/install-sql-server.md)   
 [Instalar o SQL Server do prompt de comando](./install-sql-server-from-the-command-prompt.md)   
 [Recursos compatíveis com as edições do SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md) e [Recursos compatíveis com as edições do SQL Server 2019](../../sql-server/editions-and-components-of-sql-server-version-15.md)
  
