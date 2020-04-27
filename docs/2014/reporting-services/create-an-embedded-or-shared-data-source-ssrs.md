---
title: Criar uma fonte de dados inserida ou compartilhada (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], creating
ms.assetid: b111a8d0-a60d-4c8b-b00a-51644b19c34b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 088889518d88c5fd45f988fe03185e22f041b627
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109662"
---
# <a name="create-an-embedded-or-shared-data-source-ssrs"></a>Criar uma fonte de dados inserida ou compartilhada (SSRS)
  Uma fonte de dados de relatório especifica um nome e informações de conexão. O [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] dá suporte a dois tipos de fontes de dados: inserida e compartilhada. Um fonte de dados inserida é definida em uma definição de relatório e usada apenas por esse relatório. Uma fonte de dados compartilhada é definida como um item separado e pode ser usada por vários relatórios. Para obter mais informações, consulte [conexões de dados ou fontes de dados inseridas e Compartilhadas &#40;Construtor de relatórios e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 No Construtor de Relatórios, você navega para o servidor de relatório ou site do SharePoint e seleciona fontes de dados ou cria fontes de dados inseridas. Não é possível criar fontes de dados compartilhadas no Construtor de Relatórios.  
  
 No Designer de Relatórios, é possível criar fontes de dados compartilhadas ou inseridas. No painel dados do relatório, comece a criar uma referência de fonte de dados e, em seguida, selecione a **nova** opção. Depois de criar a referência de fonte de dados, uma nova fonte de dados compartilhada será automaticamente adicionada ao Gerenciador de Soluções sob a pasta de Fontes de dados Compartilhadas.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
 Você também pode criar fontes de dados compartilhadas diretamente em um servidor de relatório ou no site do SharePoint. Para obter mais informações, consulte [criar, excluir ou modificar uma fonte de dados compartilhada &#40;Report Manager&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md) ou [criar e gerenciar fontes de dados compartilhadas &#40;Reporting Services no modo integrado do SharePoint&#41;](../../2014/reporting-services/create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
### <a name="to-create-an-embedded-or-shared-data-source"></a>Para criar uma fonte de dados inserida ou compartilhada  
  
1.  Na barra de ferramentas do painel dados do relatório, clique em **novo** e em **fonte de dados**. A caixa de diálogo **Propriedades da Fonte de Dados** é aberta.  
  
    > [!NOTE]  
    >   Se o painel de dados do relatório não estiver visível, clique em **Dados do Relatório** no menu **Exibir** .  
  
2.  Na caixa de texto **Nome** , digite um nome para a fonte de dados ou aceite o padrão. O nome da fonte de dados é usado internamente no relatório. Para fins de esclarecimento, recomendamos que o nome da fonte de dados contenha o nome do banco de dados especificado na cadeia de conexão.  
  
3.  Para uma fonte de dados inserida, verifique se a **conexão inserida** está selecionada.  
  
    1.  Na lista suspensa **Tipo** , selecione um tipo de fonte de dados; por exemplo, **Microsoft SQL Server** ou **OLE DB**.  
  
    2.  Especifique uma cadeia de conexão usando uma das seguintes alternativas:  
  
    -   Digite a cadeia de conexão diretamente na caixa de texto **Cadeia de conexão** . Para obter uma lista de cadeias de conexão de exemplo, consulte [conexões de dados, fontes de dados e cadeias de conexão em Construtor de relatórios](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-report-builder.md) ou [conexões de dados, fontes de dados e cadeias de conexão no Reporting Services](../../2014/reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
    -   Clique no botão de expressão (**fx)** para criar uma expressão que seja avaliada como uma cadeia de conexão. Na caixa de diálogo **Expressão** , digite a expressão no painel Expressão. [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
    -   Clique em **Editar** para abrir a caixa de diálogo **Propriedades de Conexão** para o tipo de fonte de dados escolhido na etapa 2.  
  
         Preencha os campos na caixa de diálogo **Propriedades de Conexão** , conforme adequado, para o tipo de fonte de dados. As propriedades de conexão incluem o tipo de fonte de dados, o nome da fonte de dados e as credenciais a serem usadas. Depois de especificar valores nesta caixa de diálogo, clique em **Testar Conexão** para verificar se a fonte de dados está disponível e se as credenciais especificadas estão corretas. Para obter mais informações sobre tipos de fonte de dados específicos, consulte os tópicos em [Adicionar dados de fontes de dados externas &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md).  
  
4.  Para uma fonte de dados compartilhada, verifique se a **referência usar fonte de dados compartilhada** está selecionada.  
  
    1.  Clique em **Novo**. Na caixa de diálogo de propriedades **Fonte de Dados Compartilhada** , siga as etapas 2 e 3 para criar uma nova fonte de dados.  
  
    2.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
         A nova fonte de dados compartilhada é exibida na pasta Fontes de Dados Compartilhada no Gerenciador de Soluções.  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
     A fonte de dados será exibida no painel de dados do relatório. No painel de dados do relatório, uma fonte de dados compartilhada aponta para a definição da fonte de dados. Em Construtor de Relatórios, a definição da fonte de dados está em um servidor de relatório ou site do SharePoint. No Designer de Relatórios, a definição da fonte de dados compartilhada é um arquivo no Gerenciador de Soluções sob a pasta Fonte de Dados Compartilhada.  
  
### <a name="to-import-an-existing-data-source-in-report-designer"></a>Para importar uma origem de dados existente no Designer de Relatórios  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Fontes de Dados Compartilhadas** no projeto do servidor de relatório e clique em **Adicionar Item Existente**. A caixa de diálogo **Adicionar Item Existente** será aberta.  
  
2.  Navegue até um arquivo de fonte de dados Compartilhada de Definição de Relatório (rds) e clique em **Abrir**.  
  
3.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-convert-an-embedded-data-source-to-a-shared-data-source-in-report-designer"></a>Para converter uma fonte de dados inserida em uma fonte de dados compartilhada no Designer de Relatórios  
  
-   No painel dados do relatório, clique com o botão direito do mouse na fonte de dados e clique em **converter em fonte de dados compartilhada**.  
  
### <a name="to-convert-a-shared-data-source-to-an-embedded-data-source-in-report-builder"></a>Para converter uma fonte de dados compartilhada em uma fonte de dados inserida no Construtor de Relatórios  
  
-   No painel dados do relatório, clique com o botão direito do mouse na fonte de dados e abra **Propriedades da fonte de dados**.  
  
-   Clique em **conexão inserida** e conclua a criação da fonte de dados inserida, conforme descrito em um procedimento anterior.  
  
## <a name="see-also"></a>Consulte Também  
 [Armazenar credenciais em uma fonte de dados Reporting Services](report-data/store-credentials-in-a-reporting-services-data-source.md)   
 [Conexões de dados ou fontes de dados inseridas e compartilhadas &#40;Construtor de Relatórios e SSRS&#41;](../../2014/reporting-services/embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md)   
 [Converter uma fonte de dados de &#40;s incorporados para compartilhados Construtor de Relatórios e SSRS&#41;](report-data/convert-data-sources-report-builder-and-ssrs.md)   
 [Associar um relatório ou modelo a uma fonte de dados compartilhada &#40;SSRS&#41;](report-data/bind-a-report-or-model-to-a-shared-data-source-ssrs.md)   
 [Configurar as propriedades da fonte de dados para um relatório &#40;Report Manager&#41;](report-data/configure-data-source-properties-for-a-report-report-manager.md)   
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](create-deploy-and-manage-mobile-and-paginated-reports.md)  
  
  
