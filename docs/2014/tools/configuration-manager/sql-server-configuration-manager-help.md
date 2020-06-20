---
title: Ajuda do SQL Server Configuration Manager | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Configuration Manager, help
ms.assetid: 6e909911-39a6-469b-b22a-3afdfd08a30b
author: stevestein
ms.author: sstein
ms.openlocfilehash: e72dc4e7e589359d59d16ea7eae8a131689045d3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85000678"
---
# <a name="sql-server-configuration-manager-help"></a>Ajuda do SQL Server Configuration Manager
  Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para configurar os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e configurar a conectividade de rede. Para criar ou gerenciar objetos de banco de dados, configurar a segurança e escrever consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] , use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte os Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Esta seção contém os tópicos da Ajuda F1 para as caixas de diálogo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
> [!NOTE]  
>  O Configuration Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode configurar versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores à [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="services"></a>Serviços  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager gerencia serviços relacionados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Embora muitas dessas tarefas possam ser realizadas com a caixa de diálogo Serviços do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, é importante observar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager executa operações adicionais nos serviços que gerencia, como aplicar as permissões corretas quando a conta do serviço é alterada. O uso da caixa de diálogo normal Serviços do Windows para configurar quaisquer serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderia prejudicar o funcionamento do serviço.  
  
 Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas de serviços:  
  
-   Iníciar, parar e pausar serviços  
  
-   Configurar serviços para iniciar automática ou manualmente, desabilitar os serviços ou alterar outras configurações de serviço  
  
-   Alterar as senhas das contas usadas pelos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando sinalizadores de rastreamento (parâmetros de linha de comando)  
  
-   Exibir as propriedades dos serviços  
  
## <a name="sql-server-network-configuration"></a>Configuração de rede do SQL Server  
 Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas relacionadas aos serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador:  
  
-   Habilitar ou desabilitar um protocolo de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Configurar um protocolo de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
> [!NOTE]  
>  Para obter um breve tutorial sobre como configurar protocolos e conectar-se ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], consulte [Tutorial: Introdução ao mecanismo de banco de dados](../../relational-databases/tutorial-getting-started-with-the-database-engine.md).  
  
## <a name="sql-server-native-client-configuration"></a>Configuração do SQL Server Native Client  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conectam ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando a biblioteca de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para as seguintes tarefas relacionadas aos aplicativos clientes neste computador:  
  
-   Para aplicativos cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neste computador, especifique a ordem dos protocolos, ao conectar instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Configure protocolos de conexão de cliente.  
  
-   Para aplicativos cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , crie aliases para instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para que os clientes possam se conectar usando uma cadeia de conexão padrão.  
  
 Para obter mais informações sobre cada uma dessas tarefas, consulte a ajuda F1 de cada tarefa.  
  
#### <a name="to-open-sql-server-configuration-manager"></a>Para abrir o SQL Server Configuration Manager  
  
-   No menu **Iniciar** , aponte para **Todos os Programas**, aponte para **Microsoft SQL Server** (versão), aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
## <a name="see-also"></a>Consulte Também  
 [Serviços SQL Servers](../../../2014/tools/configuration-manager/sql-server-services.md)   
 [Configuração de rede SQL Server](sql-server-network-configuration.md)   
 [Configuração do SQL Native Client 11,0](../../../2014/tools/configuration-manager/sql-native-client-11-0-configuration.md)   
 [Escolhendo um protocolo de rede](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
