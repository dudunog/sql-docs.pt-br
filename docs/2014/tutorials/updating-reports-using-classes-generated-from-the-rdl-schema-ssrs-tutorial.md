---
title: Atualizando relatórios usando classes geradas do esquema RDL (tutorial do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RDL [Reporting Services], generating
- RDL [Reporting Services], tutorials
- RDL [Reporting Services], serializing
ms.assetid: 8f81d48f-7ab9-4ef8-bce0-7d16d9a47fbd
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 313a5268b754089d4ca8964328d53cb23ec6edd1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62746110"
---
# <a name="updating-reports-using-classes-generated-from-the-rdl-schema-ssrs-tutorial"></a>Atualizando Relatórios por Meio de Classes Geradas a Partir do Esquema RDL (Tutorial SSRS)
  Este tutorial ilustra como usar a ferramenta de definição de esquema XML (XSD. exe) para gerar classes que permitem serializar e desserializar arquivos de definição de relatório (. RDL e. rdlc) [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] <xref:System.Xml.Serialization.XmlSerializer> com a classe.  
  
## <a name="what-you-will-learn"></a>O que você aprenderá  
 No decorrer deste tutorial, você executará estas atividades:  
  
-   Crie um aplicativo usando o [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] modelo de projeto de aplicativo de console.  
  
-   Gere classes do esquema RDL (Report Definition Language) usando a ferramenta **XSD** .  
  
-   Conecte-se a um servidor de relatório e recupere uma definição de relatório.  
  
-   Escreva código para atualizar o arquivo de definição de relatório.  
  
-   Salve a definição de relatório atualizada no servidor de relatório.  
  
-   Executar o aplicativo de esquema RDL (VB/C#).  
  
> [!NOTE]  
>  Os exemplos de código fornecidos neste tutorial poderão falhar para relatórios que não têm nenhuma descrição. A falha ocorre porque a propriedade de descrição não existe para os relatórios sem a descrição especificada.  
  
## <a name="requirements"></a>Requisitos  
 Para concluir o tutorial, você deve ter o seguinte:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)].  
  
-   Permissões suficientes para acessar e publicar relatórios no serviço Web Servidor de Relatórios no computador em que o servidor de relatório está localizado.  
  
-   O banco de dados de exemplo [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] instalado em uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Um relatório instalado no servidor de relatório. Este tutorial usa o relatório de exemplo, Company Sales 2012. Para obter mais informações sobre relatórios de exemplo, consulte [SQL Server Reporting Services exemplos de produto](https://go.microsoft.com/fwlink/?LinkId=177889).  
  
> [!NOTE]  
>  Os exemplos não são instalados automaticamente durante a instalação, mas podem ser instalados a qualquer momento. Para obter informações sobre exemplos, consulte [SQL Server exemplos de produtos](https://go.microsoft.com/fwlink/?LinkId=182887).  
  
 **Tempo estimado para concluir o tutorial:** 30 minutos  
  
## <a name="tasks"></a>Tarefas  
 [Lição 1: Criar o projeto do Visual Studio de esquema RDL](../../2014/tutorials/lesson-1-create-the-rdl-schema-visual-studio-project.md)  
  
 [Lição 2: Gerar classes do esquema RDL usando a ferramenta xsd](../../2014/tutorials/lesson-2-generate-classes-from-the-rdl-schema-using-the-xsd-tool.md)  
  
 [Lição 3: Carregar uma definição de relatório do Servidor de Relatório](../../2014/tutorials/lesson-3-load-a-report-definition-from-the-report-server.md)  
  
 [Lição 4: Atualizar a definição do relatório programaticamente](../../2014/tutorials/lesson-4-update-the-report-definition-programmatically.md)  
  
 [Lição 5: Publicar a definição de relatório no servidor de relatório](../../2014/tutorials/lesson-5-publish-the-report-definition-to-the-report-server.md)  
  
 [Lição 6: executar o aplicativo de esquema RDL &#40;VB-C&#35;&#41;](../../2014/tutorials/lesson-6-run-the-rdl-schema-application-vb-csharp.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Linguagem RDL &#40;SSRS&#41;](../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
