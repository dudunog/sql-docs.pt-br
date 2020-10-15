---
title: Tipo de conexão OLE DB | Microsoft Docs
description: Use as informações fornecidas neste artigo sobre o tipo de conexão OLE DB para aprender a criar uma fonte de dados.
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: d00cb13b-e1c2-4300-a195-3da1430a2df1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: bff06284226c67a0f784b9e77bbe85dd056edb09
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891136"
---
# <a name="ole-db-connection-type-ssrs"></a>Tipo de conexão OLE DB (SSRS)
  Para incluir dados de um provedor de dados OLE DB, é necessário ter um conjunto de dados baseado em uma fonte de dados de relatório do tipo OLE DB. Esse tipo de fonte de dados interna tem como base a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] extensão de processamento de dados OLE DB.  
  
 OLE DB é uma tecnologia de acesso a dados que permite aos clientes conectar-se a vários provedores de dados. Depois que você selecionar o tipo de fonte de dados OLE DB, deverá selecionar um provedor de dados específico. O suporte a recursos, como parâmetros e credenciais, depende do provedor de dados selecionado.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="connection-string"></a><a name="Connection"></a> Cadeia de Conexão  
 A cadeia de caracteres de conexão da extensão de processamento de dados OLE DB depende do provedor de dados desejado. Uma cadeia de caracteres de conexão típica contém pares de nome/valor que são suportados pelo provedor de dados. Por exemplo, a cadeia de caracteres de conexão a seguir especifica o provedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e do banco de dados AdventureWorks:  
  
```  
Provider=SQLNCLI10.1;Data Source=server; Initial Catalog=AdventureWorks  
```  
  
 A cadeia de conexão utilizada depende da fonte de dados externa à qual você está se conectando. Para definir as propriedades da cadeia de caracteres de conexão específicas de um provedor de dados, na página **Geral** da caixa de diálogo **Propriedades da Fonte de Dados** , clique no botão **Construir** para abrir a caixa de diálogo **Propriedades da Conexão** . Defina propriedades de fonte de dados estendidas através da caixa de diálogo **Propriedades de Link de Dados** .  
  
 Para ver exemplos de cadeias de conexão, confira [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
  
##  <a name="credentials"></a><a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Para obter mais informações, consulte [Especificar informações de credenciais e de conexão para fontes de dados de relatório](specify-credential-and-connection-information-for-report-data-sources.md).  
  
###### <a name="special-characters-in-a-password"></a>Caracteres especiais em uma senha  
 Se você configurar a fonte de dados OLE DB para exigir uma senha ou para incluir uma senha na cadeia de conexão e um usuário inserir a senha com caracteres especiais, como sinais de pontuação, alguns drivers de fonte de dados subjacentes não conseguirão validar os caracteres especiais. Quando você processar o relatório, a mensagem "Senha inválida" poderá indicar esse problema.  
  
> [!NOTE]  
>  Não é recomendável a inclusão de informações de logon, como senhas, na cadeia de conexão. O Construtor de Relatórios fornece uma guia separada na caixa de diálogo **Fonte de Dados** que pode ser usada para inserir credenciais.  
  
  
##  <a name="parameters"></a><a name="Parameters"></a> Parâmetros  
 Alguns provedores OLE DB oferecem suporte a parâmetros não nomeados, e não a parâmetros nomeados. Os parâmetros são transmitidos por posição, através de um espaço reservado na consulta. O caractere de espaço reservado é determinado pela sintaxe suportada pelo provedor de dados.  
  
  
##  <a name="remarks"></a><a name="Remarks"></a> Comentários  
 OLEDB é uma tecnologia nativa para criação de provedores de dados para fontes de dados específicas. A tecnologia OLEDB é baseada em interfaces COM (Component Object Model). A tecnologia OLEDB é posterior à ODBC e anterior aos provedores de dados ADO.NET. Os provedores de dados OLEDB são registrados com o sistema operacional, como qualquer outro componente COM. Há provedores de dados OLEDB disponibilizados pela Microsoft e por fornecedores terceirizados. A Microsoft fornece também o MSDASQL, um provedor de dados OLEDB que faz a comunicação com drivers ODBC. Para obter mais informações, consulte [Tipo de conexão ODBC &#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md).  
  
 Para recuperar os dados desejados com êxito, é necessário fornecer uma sintaxe de consulta que seja suportada pelo provedor de dados. O suporte a parâmetros varia de acordo com o provedor de dados. Para obter mais informações, consulte os tópicos específicos do provedor de dados selecionado. Por exemplo:  
  
-   [Provedor OLE DB do Analysis Services &#40;Analysis Services – Dados Multidimensionais&#41;](/analysis-services/instances/data-providers-used-for-analysis-services-connections
)  
   
  
-   [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
 Para obter mais informações sobre os provedores de dados específicos de OLE DB, consulte [Fontes de dados compatíveis com o Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
  
##  <a name="how-to-topics"></a><a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="related-sections"></a><a name="Related"></a> Seções relacionadas  
 Estas seções da documentação fornecem informações conceituais detalhadas sobre dados de relatório, bem como informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados compatíveis com o Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
