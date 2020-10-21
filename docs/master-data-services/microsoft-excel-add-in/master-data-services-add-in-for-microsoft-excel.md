---
title: Visão geral
description: Saiba como carregar dados de Master Data Services no Excel e publicá-los de volta no Master Data Services usando o Suplemento do Master Data Services para Excel.
ms.custom: microsoft-excel-add-in, seo-lt-2019
ms.date: 07/25/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 33d9c8fc-9602-494d-b9ab-8f0f42785974
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ec0059471e10db953db26cfdd4c7b620a3378316
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "92257785"
---
# <a name="master-data-services-add-in-for-microsoft-excel"></a>Suplemento do Master Data Services para Microsoft Excel

[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], você pode carregar listas filtradas de dados do MDS no Excel, em que pode trabalhar com elas da mesma maneira como trabalharia com outros dados. Quando você terminar, poderá publicar os dados no MDS novamente, onde serão armazenados centralmente. A segurança determina quais dados você pode exibir e atualizar.  
  
 Se você for um administrador, também poderá usar o [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] para novas entidades e atributos, e carregá-los com os dados. Isso elimina a necessidade de usar outras ferramentas para carregar dados em seus modelos.  
  
 No [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)], você pode usar o DQS (Data Quality Services) para combinar os dados antes de carregá-los no MDS. Isso ajuda a evitar dados duplicados no MDS.  

## <a name="downloads"></a>Downloads 
>*  Baixe o Suplemento Master Data Services para Excel para SQL Server 2016 SP2 [dessa página do Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=56838). 
>* Baixe o [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../../includes/ssmdsxls-md.md)] para o SQL Server 2017 [nesta página do Centro de Download da Microsoft](https://go.microsoft.com/fwlink/?linkid=836867).
>*  Baixe o Suplemento do Master Data Services para Excel para o SQL Server 2019 CTP [desta página do centro de download da Microsoft](https://go.microsoft.com/fwlink/?linkid=2086948). 
 
  
## <a name="terms"></a>Termos  
 No suplemento, você poderá encontrar os termos a seguir. Para obter mais informações sobre esses conceitos, consulte [Visão geral do MDS &#40;Master Data Services&#41;](../../master-data-services/master-data-services-overview-mds.md).  
  
-   O *MDS repository* é onde são armazenados todos os dados mestre. É um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é configurado para armazenar dados do MDS. Para trabalhar com os dados do repositório, você carrega os dados no Excel, ao terminar o trabalho, você publica as alterações no repositório novamente. Os administradores podem adicionar novas entidades e atributos ao repositório.  
  
-   *Dados gerenciados no MDS* são dados armazenados no repositório do MDS e que são carregados no Excel, em que os dados são exibidos como linhas realçadas. Você pode adicionar dados que não sejam gerenciados no MDS à sua planilha, e eles não serão afetados quando você atualizar os dados gerenciados no MDS.  
  
-   Um *model* é um contêiner de dados. As versões desses contêineres podem ser criadas, e normalmente a última versão é o mais recente. Para obter mais informações, consulte [Modelos &#40;Master Data Services&#41;](../../master-data-services/models-master-data-services.md).  
  
-   Uma *entity* é uma lista de dados. Você pode pensar em uma entidade como uma tabela em um banco de dados. Por exemplo, a entidade **Cor** pode conter uma lista de cores. Para obter mais informações, consulte [Entidades &#40;Master Data Services&#41;](../../master-data-services/entities-master-data-services.md).  
  
-   Um *membro* é uma linha de dados (um registro). Cada entidade contém membros. Um exemplo de membro é **Azul**. Para obter mais informações, consulte [Membros &#40;Master Data Services&#41;](../../master-data-services/members-master-data-services.md).  
  
-   Um *attribute* é uma coluna de dados. Cada membro possui atributos. Por exemplo, o atributo de **código** para o membro **azul** é **B**. Para obter mais informações sobre atributos, consulte [atributos &#40;Master Data Services&#41;](../../master-data-services/attributes-master-data-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Crie uma conexão com um repositório do [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] .|[Conectar-se a um repositório do MDS &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connect-to-an-mds-repository-mds-add-in-for-excel.md)|  
|Carregue os dados gerenciados no MDS no Excel.|[Exportar dados para o Excel do Master Data Services](../../master-data-services/microsoft-excel-add-in/export-data-to-excel-from-master-data-services.md)|  
|Salve um arquivo de consulta de atalho que você possa usar para abrir os dados gerenciados no MDS exibidos atualmente no futuro.|[Salvar um arquivo de consulta de atalho &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/save-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Compartilhe atalhos com outros usuários.|[Enviar um arquivo de consulta de atalho por email &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/email-a-shortcut-query-file-mds-add-in-for-excel.md)|  
|Veja todas as alterações que foram feitas em um membro.|[Exibir todas as anotações ou transações de um membro &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/view-all-annotations-or-transactions-for-a-member-mds-add-in-for-excel.md)|  
|Antes de publicar novos dados, descubra se há duplicação.|[Corresponder dados semelhantes &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/match-similar-data-mds-add-in-for-excel.md)|  
|Publique dados de uma planilha no repositório do MDS.|[Importar dados do Excel para o Master Data Services &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/import-data-from-excel-to-master-data-services-mds-add-in-for-excel.md)|  
|Crie uma nova entidade com dados na planilha. (Somente para administradores)|[Criar uma entidade &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-an-entity-mds-add-in-for-excel.md)|  
|Crie um atributo baseado em domínio, também conhecido como lista restrita. (Somente para administradores)|[Criar um atributo baseado em domínio &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/create-a-domain-based-attribute-mds-add-in-for-excel.md)|  
|Defina as propriedades para carregar e publicar dados no Suplemento do Master Data Services para Excel. (Somente para administradores)|[Definindo propriedades para o Suplemento do Master Data Services para Excel](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Conexões &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/connections-mds-add-in-for-excel.md)  
  
-   [Visão geral: Exportando dados para o Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-exporting-data-to-excel-mds-add-in-for-excel.md)  
  
-   [Arquivos de consulta de atalho &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/shortcut-query-files-mds-add-in-for-excel.md)  
  
-   [Atualizando dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/refreshing-data-mds-add-in-for-excel.md)  
  
-   [Visão geral: Importando dados do Excel &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/overview-importing-data-from-excel-mds-add-in-for-excel.md)  
  
-   [Validando dados &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/validating-data-mds-add-in-for-excel.md)  
  
-   [Correspondência de qualidade de dados no Suplemento do MDS para Excel](../../master-data-services/microsoft-excel-add-in/data-quality-matching-in-the-mds-add-in-for-excel.md)  
  
-   [Criando um modelo &#40;Suplemento MDS para Excel&#41;](../../master-data-services/microsoft-excel-add-in/building-a-model-mds-add-in-for-excel.md)  
  
-   [Definindo propriedades para o Suplemento do Master Data Services para Excel](../../master-data-services/microsoft-excel-add-in/setting-properties-for-master-data-services-add-in-for-excel.md)  
  
-   [Segurança &#40;Master Data Services&#41;](../../master-data-services/security-master-data-services.md)  
  
  
