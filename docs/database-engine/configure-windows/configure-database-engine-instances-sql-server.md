---
title: Configurar instâncias do Mecanismo de Banco de Dados (SQL Server) | Microsoft Docs
description: Familiarize-se com tarefas de configuração do SQL Server para poder configurar uma instância do Mecanismo de Banco de Dados para atender aos requisitos de desempenho e disponibilidade.
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 84e36fcb-2c78-48e8-8e4b-bf784a3ee557
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b2b3900c41067e7f46f392ceab913f1d8d096816
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751928"
---
# <a name="configure-database-engine-instances-sql-server"></a>Configurar instâncias do mecanismo de banco de dados (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Cada instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ser configurada para satisfazer os requisitos de desempenho e disponibilidade definidos para os bancos de dados hospedados pela instância. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] inclui opções de configuração que controlam comportamentos como uso de recurso e a disponibilidade de recursos como auditoria ou recursão de gatilho.  
  
## <a name="instance-configuration"></a>Configuração de Instância  
 Quando um banco de dados é implantado na produção, em geral há um SLA (acordo em nível de serviço) que define áreas como os níveis de desempenho necessários do banco de dados e o nível de disponibilidade exigido pelo banco de dados. As condições do SLA normalmente orientam requisitos de configuração da instância.  
  
 Uma instância costuma ser configurada logo após ser instalada. A configuração inicial normalmente é determinada pelos requisitos de SLA dos tipos de bancos de dados planejados para serem implantados na instância. Depois que os bancos de dados forem implantados, os administradores de banco de dados monitorarão o desempenho da instância e ajustarão os parâmetros de configuração, quando necessário, se a métrica de desempenho mostrar que a instância não está satisfazendo os requisitos de SLA.  
  
## <a name="configuration-tasks"></a>Tarefas de configuração  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve as várias opções de configuração de instância e como exibir ou alterar essas opções.|[Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)|  
|Descreve como exibir e configurar os locais padrão de novos arquivos de log e de dados na instância.|[Exibir ou alterar os locais padrão de arquivos de log e de dados &#40;SQL Server Management Studio&#41;](../../database-engine/configure-windows/view-or-change-the-default-locations-for-data-and-log-files.md)|  
|Descreve como configurar o SQL Server para usar o soft-NUMA.|[Soft-NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)|  
|Descreve como mapear uma porta TCP/IP para afinidade de nó NUMA (acesso não uniforme a memória).|[Mapear portas TCP/IP para nós NUMA &#40;SQL Server&#41;](../../database-engine/configure-windows/map-tcp-ip-ports-to-numa-nodes-sql-server.md)|  
|Descreve como habilitar a política Bloquear Páginas na Memória do Windows Essa política determina quais contas podem usar um processo para manter dados na memória física, impedindo que o sistema faça a paginação dos dados para a memória virtual em disco.|[Habilitar a opção Bloquear Páginas na Memória &#40;Windows&#41;](../../database-engine/configure-windows/enable-the-lock-pages-in-memory-option-windows.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Instâncias do mecanismo de banco de dados &#40;SQL Server&#41;](../../database-engine/configure-windows/database-engine-instances-sql-server.md)  
  
  
