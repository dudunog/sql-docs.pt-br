---
title: Gerenciador de Conexões do SQL Server Compact Edition | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Compact, connection manager
- connections [Integration Services], SQL Server Compact
- connection managers [Integration Services], SQL Server Compact
ms.assetid: ba627d4d-41f4-49fc-a921-f534cde67770
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a8242de8a7374fec7bad5e0eb4fabf96264cecc1
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85438323"
---
# <a name="sql-server-compact-edition-connection-manager"></a>Gerenciador de Conexões do SQL Server Compact Edition
  Um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact permite que um pacote se conecte a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact. O destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui usa esse gerenciador de conexões para carregar dados em uma tabela no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  Em um computador de 64 bits, você deve executar pacotes que se conectam a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact no modo de 32 bits. O provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usa para se conectar a fontes de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, só está disponível na versão de 32 bits.  
  
## <a name="configuration-the-sql-server-compact-edition-connection-manager"></a>Configuração do gerenciador de conexões do SQL Server Compact Edition  
 Quando você adiciona um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de conexões compacta a um pacote, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o cria um Gerenciador de conexões que será resolvido para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão compacta em tempo de execução, define as propriedades do Gerenciador de conexões e adiciona o Gerenciador de conexões à `Connections` coleção no pacote.  
  
 A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `SQLMOBILE`.  
  
 Você pode configurar um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão que especifique o local do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
-   Forneça uma senha para um banco de dados protegido por senha.  
  
-   Especifique o servidor no qual o banco de dados está armazenado.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página de Conexão&#41;](../sql-server-compact-edition-connection-manager-editor-connection-page.md)  
  
-   [Editor do Gerenciador de Conexões do SQL Server Compact Edition &#40;Página Tudo&#41;](../sql-server-compact-edition-connection-manager-editor-all-page.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
