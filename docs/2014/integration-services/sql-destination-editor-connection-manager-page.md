---
title: Editor de destino SQL (página Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlserverdestadapter.connection.f1
helpviewer_keywords:
- SQL Server Destination Editor
ms.assetid: 423e1654-54af-47c6-ab6f-98670534557d
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 44b7a2b45ca77af87457ae0f4e908ec0a667ff79
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962806"
---
# <a name="sql-destination-editor-connection-manager-page"></a>Editor do Destino SQL (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destinos SQL** para especificar informações de fonte de dados e visualizar os resultados. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] destino carrega dados em tabelas ou exibições em um banco de dados [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações sobre destino do SQL Server, consulte [SQL Server Destination](data-flow/sql-server-destination.md).  
  
## <a name="options"></a>Opções  
 **Gerenciador de conexões OLE DB**  
 Selecione uma conexão existente na lista ou crie uma nova conexão clicando em **Novo**.  
  
 **Novo**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
 **Use uma tabela ou exibição**  
 Selecione uma tabela ou exibição existente na lista ou crie uma nova conexão clicando em **Novo**.  
  
 **Novo**  
 Crie uma nova tabela usando a caixa de diálogo **Criar Tabela** .  
  
> [!NOTE]  
>  Quando você clica em **novo**, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o gera uma instrução de CREATE TABLE padrão com base na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Visualização**  
 Visualize os resultados usando a caixa de diálogo **Visualizar Resultados da Consulta** . A visualização pode exibir até 200 linhas.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Página Mapeamentos de &#40;do editor de destinos SQL&#41;](../../2014/integration-services/sql-destination-editor-mappings-page.md)   
 [Editor de destinos SQL &#40;página avançado&#41;](../../2014/integration-services/sql-destination-editor-advanced-page.md)   
 [Carregar dados em massa por meio do destino do SQL Server](data-flow/bulk-load-data-by-using-the-sql-server-destination.md)  
  
  
