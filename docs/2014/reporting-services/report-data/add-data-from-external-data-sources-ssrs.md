---
title: Adicionar dados de fontes de dados externas (SSRS)
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/27/2017
ms.openlocfilehash: 54358529577061ad99c634fa6cc4ce9d98792e0c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67412687"
---
# <a name="add-data-from-external-data-sources-ssrs"></a>Adicionar dados de fontes de dados externas (SSRS)

Para recuperar dados de uma fonte de dados externa, use uma conexão de dados. As informações da conexão de dados normalmente são fornecidas pelo proprietário da fonte de dados externa que é responsável por conceder permissões e especificar os tipos de credenciais a serem usados. As informações de conexão de dados são salvas como uma fonte de dados de relatório. O tipo de fonte de dados especifica a extensão de processamento de dados a ser usada para recuperar a fonte de dados.  

##  <a name="understanding-data-access-technology"></a><a name="DataAccess"></a>Noções básicas sobre a tecnologia de acesso a dados  

A recuperação de dados para um conjunto de dados de relatório requer várias camadas de software de acesso a dados. A lista a seguir fornece uma descrição simples de como os relatórios funcionam com as tecnologias de acesso a dados:  

-   **Aplicativo e interface do usuário** O aplicativo Construtor de Relatórios usado para criar uma fonte de dados, adicionar uma referência a uma fonte de dados compartilhada, adicionar um conjunto de dados compartilhado ou adicionar uma parte de relatório que inclui as fontes de dados e conjuntos de dados dos quais ele depende.  

-   **Elementos de definição de relatório** As fontes de dados e os conjuntos de dados fazem parte da definição de relatório. Depois que um relatório é publicado em um servidor de relatório, as fontes de dados compartilhadas e os conjuntos de dados compartilhados são gerenciados de forma independente na definição de relatório.  

  -   **Fonte de dados e fonte de dados compartilhada** Parte de uma definição de relatório que inclui as informações sobre o tipo de extensão de processamento de dados, as informações de conexão e a autenticação.  

  -   **Conjunto de dados e coleção de campos** Parte de uma definição de relatório que inclui a consulta, a coleção de campos e os tipos de dados de campos.  

-   **Extensões de dados do Reporting Services** Extensões de dados internas que são instaladas com Construtor de Relatórios. Uma extensão de dados fornece a funcionalidade que cuida de autenticação, agregações de servidor e parâmetros multivalor.  

-   **Provedor de dados** O software que gerencia a conexão e a recuperação de dados da fonte de dados externa. O provedor de dados define a sintaxe da cadeia de conexão. A maioria das extensões de dados é criada sobre uma camada de provedor de dados.  

-   **Fonte de dados externa** O local do qual se recupera dados de relatório, por exemplo, um banco de dados, um arquivo, um cubo ou um serviço Web.  

> [!NOTE]  
>  Quando você não está conectado a um servidor de relatório, pode escolher as extensões de dados instaladas com o Construtor de Relatórios. Você acessa os dados como um usuário único usando as credenciais de seu computador. Quando você está conectado a um servidor de relatório, pode escolher as extensões de dados instaladas no servidor de relatório. Você acessa os dados como um de vários usuários que executam o relatório e usa as credenciais no servidor de relatório. Para obter mais informações, consulte [Especificar as credenciais no Construtor de Relatórios](../specify-credentials-in-report-builder.md).  

##  <a name="understanding-report-data"></a><a name="ReportData"></a> Compreendendo os dados de relatório  
Na forma mais simples, um relatório exibe dados de um conjunto de dados de relatório em uma região de dados na página do relatório, ou seja, em uma única tabela, gráfico, matriz ou outro tipo de região de dados de relatório. Os dados em um conjunto de dados de relatório provêm do primeiro conjunto de resultados retornado de um único comando de consulta que é executado com acesso somente leitura para uma fonte de dados externa. Cada região de dados é expandidas conforme necessário para exibir todos os dados do conjunto de dados.  

Os dados em um conjunto de dados são essencialmente tabulares. As colunas são os campos da consulta de conjunto de dados. As linhas provêm das linhas no conjunto de resultados. Você pode usar os seguintes tipos de dados generalizados em um relatório:  

-   Dados retangulares. Dados de um conjunto de resultados que tem o mesmo número de colunas em cada linha.  

-   Os dados hierárquicos têm suporte como um conjunto de linhas bidimensional.  

  -   Não há suporte para hierarquias desbalanceadas, em que há um número diferente de colunas para cada linha de dados. Para algumas extensões de dados, isso tem algumas implicações.  

  -   As extensões de dados que funcionam com fontes de dados multidimensionais usam o protocolo XML for Analysis e recuperam dados como um conjunto de linhas bidimensionais e não como um conjunto de células.  

  -   A extensão de dados XML automaticamente mescla os dados XML para usá-los em um relatório. Se a primeira instância de um elemento XML não incluir todos os atributos ou suplementos, os dados talvez não estejam disponíveis como dados de relatório.  

-   Os dados recursivos possuem suporte. Um conjunto de resultados que contém uma hierarquia de dados recursiva inclui todas as informações sobre a estrutura de hierarquia em um conjunto de resultados retangular. Por exemplo, a estrutura de subordinação em uma empresa pode ser representada por uma tabela que inclui duas colunas: um funcionário e um gerente. Cada gerente também é um funcionário com um gerente. O gerente principal normalmente contém um nulo ou outro identificador indicando que esse funcionário não tem gerente.  



##  <a name="working-with-data-types"></a><a name="DataTypes"></a>Trabalhando com tipos de dados  
Quando você cria um conjunto de dados, os tipos de dados dos campos são mapeados para o subconjunto de tipos de dados CLR do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Os tipos de dados que não puderem ser claramente mapeados serão retornados como cadeias de caracteres. Para obter mais informações sobre como trabalhar com tipos de dados do campo, consulte [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md). Quando você criar um parâmetro, o tipo de dados deverá ser um dos tipos de dados de definição de relatório suportados. Para obter mais informações sobre como mapear tipos de dados do provedor de dados para um parâmetro de relatório, consulte [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md).  



##  <a name="how-to-topics"></a><a name="HowTo"></a>Tópicos de instruções  
Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  

[Adicionar e verificar uma conexão de dados ou uma fonte de dados &#40;Construtor de Relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  

[Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  

[Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  

## <a name="in-this-section"></a><a name="InThisSection"></a>Nesta seção  

Os tópicos a seguir fornecem informações sobre cada extensão de dados interna.  

|Tópico|Tipo de fonte de dados|  
|-----------|----------------------|  
|[O tipo de conexão do SQL Server &#40;SSRS&#41;](sql-server-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|[Tipo de conexão Analysis Services para MDX &#40;SSRS&#41;](analysis-services-connection-type-for-mdx-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[Tipo de conexão PowerPivot &#40;&#41;SSRS](power-pivot-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|  
|[Tipo de conexão de lista do SharePoint &#40;SSRS&#41;](sharepoint-list-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Lista do SharePoint|  
|[Tipo de conexão do SQL Azure &#40;SSRS&#41;](sql-azure-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDS](../../includes/sssds-md.md)]|  
|[Tipo de conexão do SQL Server Parallel Data Warehouse &#40;SSRS&#41;](sql-server-parallel-data-warehouse-connection-type-ssrs.md)|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../../includes/ssdwfull-md.md)]|  
|[Tipo de conexão SAP NetWeaver BI &#40;SSRS&#41;](sap-netweaver-bi-connection-type-ssrs.md)|SAP NetWeaver BI|  
|[Tipo de conexão Hyperion Essbase &#40;SSRS&#41;](hyperion-essbase-connection-type-ssrs.md)|Hyperion Essbase|  
|[Tipo de conexão OLE DB &#40;SSRS&#41;](ole-db-connection-type-ssrs.md)|OLE DB|  
|[Tipo de Conexão ODBC &#40;SSRS&#41;](odbc-connection-type-ssrs.md)|ODBCODBC|  
|[Tipo de conexão XML &#40;SSRS&#41;](xml-connection-type-ssrs.md)|XML|  

## <a name="related-sections"></a><a name="Related"></a>Seções relacionadas  

Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  

|Tópico|Descrição|  
|-----------|-----------------|  
|[Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-datasets-ssrs.md)|Fornece uma visão geral de como acessar dados de seu relatório.|  
|[Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)|Fornece informações sobre conexões de dados e fontes de dados.|  
|[Conjuntos de itens de relatório inseridos e conjuntos de &#40;compartilhados Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)|Fornece informações sobre conjuntos de dados inseridos e compartilhados.|  
|[Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)|Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.|  
|[Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na documentação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do .|Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.|  
|[Visão geral das extensões de processamento de dados](../extensions/data-processing/data-processing-extensions-overview.md) na documentação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] nos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [do](https://go.microsoft.com/fwlink/?linkid=121312).|Fornece informações detalhadas para usuários avançados sobre extensões de dados.|  

## <a name="see-also"></a>Consulte Também  

- [Adicionar dados a um relatório &#40;Construtor de Relatórios e SSRS&#41;](report-datasets-ssrs.md)
- [Designers de Consultas &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md)