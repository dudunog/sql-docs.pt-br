---
title: Carregar dados em massa por meio do destino do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server destination
- loading data
- destinations [Integration Services], SQL Server
- inserting data
- bulk load [Integration Services]
ms.assetid: 8f982f85-a82e-4e2d-9cd8-cd2f85402d8e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38b4b61cecf57f4ce0db7152aff1bc5c08ccf500
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915498"
---
# <a name="bulk-load-data-by-using-the-sql-server-destination"></a>Carregar dados em massa por meio do destino do SQL Server

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Para adicionar e configurar um destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o pacote já deve incluir pelo menos uma tarefa de Fluxo de Dados e uma fonte de dados.  
  
### <a name="to-load-data-using-a-sql-server-destination"></a>Para carregar dados usando um destino de SQL Server  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Dados** , e então, na **Caixa de Ferramentas**, arraste o destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a superfície de design.  
  
4.  Conecte o destino a uma fonte ou a uma transformação prévia no fluxo de dados arrastando um conector para o destino.  
  
5.  Clique duas vezes no destino.  
  
6.  No **Editor de Destino do SQL Server**, na página **Gerenciador de Conexões** , selecione um gerenciador de conexões OLE DB existente ou clique em **Novo** para criar um gerenciador de conexões novo. Para obter mais informações, consulte [OLE DB Connection Manager](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
7.  Para especificar a tabela ou exibir em qual tabela serão carregados os dados, siga um destes procedimentos:  
  
    -   Selecione uma tabela ou exibição existente.  
  
    -   Clique em **Novo**e, na caixa de diálogo **Criar Tabela** , escreva uma instrução SQL que cria uma tabela ou exibição.  
  
        > [!NOTE]  
        >  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão baseada na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
8.  Clique em **Mapeamentos** e mapeie as colunas da lista **Colunas de Entrada Disponíveis** para colunas na lista **Colunas de Destino Disponíveis** arrastando colunas de uma lista para outra.  
  
    > [!NOTE]  
    >  O destino mapeia colunas do mesmo nome automaticamente.  
  
9. Clique em **Avançado** e defina as opções de carregamento em massa: **Manter identidade**, **Manter nulos**, **Bloqueio de tabela**, **Verificar restrições**e **Gatilhos**.  
  
     Opcionalmente, especifique a primeira e a última linha de entrada a serem inseridas, o número máximo de erros que podem acontecer antes da operação de inserção ser interrompida e as colunas em que a inserção é classificada.  
  
    > [!NOTE]  
    >  A ordem de classificação é determinada pela ordem em que as colunas são relacionadas.  
  
10. Clique em **OK**.  
  
11. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Destination](../../integration-services/data-flow/sql-server-destination.md)   
 [Transformações do Integration Services](../../integration-services/data-flow/transformations/integration-services-transformations.md)   
 [Caminhos do Integration Services](../../integration-services/data-flow/integration-services-paths.md)   
 [Tarefa de Fluxo de Dados](../../integration-services/control-flow/data-flow-task.md)  
  
  
