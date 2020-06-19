---
title: Recuperar e compreender os dados de alterações | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],retrieving data
ms.assetid: af366697-6942-42bb-aea5-18fdef018965
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6e4f14ae8513e62e9af4c129cc0a2aea25c88e42
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84922607"
---
# <a name="retrieve-and-understand-the-change-data"></a>Recuperar e compreender os dados de alteração
  No fluxo de dados de um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que executa uma carga incremental de dados de alteração, a primeira tarefa é executar a consulta que recupera os dados de alteração. Você executa esta consulta dentro de um componente de origem em uma tarefa Fluxo de Dados. As transformações downstream e os destinos podem ser usados para aplicar os dados de alteração em seu destino.  
  
> [!NOTE]  
>  A criação de uma consulta que contém uma função com valor de tabela é a terceira etapa no processo de criação de um pacote que execute uma carga incremental dos dados de alteração. Para obter mais informações sobre esta consulta, veja [Criar a função para recuperar os dados de alteração](create-the-function-to-retrieve-the-change-data.md). Para obter uma descrição do processo geral para criar um pacote que realiza uma carga incremental de dados de alteração, consulte [Change Data Capture &#40;SSIS&#41;](change-data-capture-ssis.md).  
  
## <a name="adding-the-data-flow-task"></a>Adicionando a tarefa Fluxo de Dados  
 No fluxo de dados do pacote, você recupera os dados de alteração, separa as linhas com base no tipo de alteração ocorrida e aplica as alterações ao destino.  
  
#### <a name="to-add-a-data-flow-task-to-the-package"></a>Adicionar uma tarefa Fluxo de Dados ao pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na guia **Fluxo de Controle** , adicione uma tarefa Fluxo de Dados.  
  
2.  Conecte a tarefa de precedência que preparou a cadeia de caracteres de consulta à tarefa Fluxo de Dados.  
  
## <a name="configuring-the-source-component-to-query-for-changes"></a>Configurando o componente de origem para a consulta de alterações  
 O componente de origem usa a cadeia de caracteres de consulta que foi preparada e armazenada em uma variável para chamar a função com valor de tabela que recupera os dados alterados.  
  
> [!NOTE]  
>  Para obter mais informações sobre a cadeia de caracteres de consulta que foi preparada e armazenada em uma variável, consulte [Preparar para consultar os dados de alteração](prepare-to-query-for-the-change-data.md). Para obter mais informações sobre a função com valor de tabela que recupera os dados de alteração, consulte [Criar a função para recuperar os dados de alteração](create-the-function-to-retrieve-the-change-data.md).  
  
#### <a name="to-configure-an-ole-db-source-to-retrieve-the-change-data"></a>Configurar uma fonte OLE DB para recuperar os dados de alteração  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], na guia **Fluxo de Dados** , adicione uma fonte OLE DB.  
  
2.  No **Editor de Origem de OLE DB**, na página **Gerenciador de Conexões** , selecione as seguintes opções:  
  
    1.  Configure uma conexão válida com o banco de dados fonte.  
  
    2.  Para **Modo de acesso a dados**, selecione o **Comando SQL a partir da variável**.  
  
    3.  Para **Nome da variável**, selecione **User::SqlDataQuery**.  
  
3.  No **Editor de Origem de OLE DB**, na página **Colunas** , verifique se todas as colunas estão mapeadas para as colunas de saída.  
  
## <a name="next-step"></a>Próxima etapa  
 Depois de configurar uma fonte de OLE DB para recuperar os dados de alteração, a próxima etapa será iniciar a criação do fluxo de dados no pacote.  
  
 **Próximo tópico:** [Processar inserções, atualizações e exclusões](process-inserts-updates-and-deletes.md)  
  
  
