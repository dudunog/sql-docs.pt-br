---
title: Caixa de diálogo Páginas de Propriedades do Projeto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rpt.rptdesigner.projectpropertypages.general.f1
helpviewer_keywords:
- Project Property Pages dialog box
ms.assetid: 209d9e22-37fc-418f-8739-83adcf447d3f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a9d66e6e5317bef72be6bba254ccca0cc82aa026
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100037"
---
# <a name="project-property-pages-dialog-box"></a>caixa de diálogo Páginas de Propriedades do Projeto
  Use as páginas de propriedades do projeto para configurar as propriedades de implantação de um projeto do Servidor de Relatório. Para abrir essa caixa de diálogo, no menu **Projeto**, clique em _\<Report Project Name>_ **Propriedades**.  
  
 Depois que você definir as propriedades de configuração, poderá selecionar uma configuração na lista suspensa **Configurações da Solução** da barra de ferramentas.  
  
## <a name="options"></a>Opções  
 **Configuração**  
 Selecione a configuração a ser editada. Inicialmente, estão disponíveis as seguintes configurações: **Debug**, **DebugLocal**e **Release**. A configuração ativa aparece primeiro; por exemplo, **Active(Debug)**.  
  
 Para ver as propriedades de mais de uma configuração ao mesmo tempo, selecione **Todas as Configurações** ou **Várias Configurações**.  
  
 Para criar configurações adicionais, clique em **Configuration Manager** na barra de ferramentas.  
  
 **Configuration Manager**  
 Gerencie configurações da solução inteira ou adicione outras configurações. Para obter mais informações, consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
 **OutputPath**  
 Digite ou cole o caminho para armazenar a definição de relatório usada na verificação da compilação, na implantação e na visualização de relatórios. O caminho deve ser diferente do caminho que você usa para o projeto e um caminho relativo que é uma pasta filho sob o caminho do projeto.  
  
> [!NOTE]  
>  Você pode usar várias configurações para alternar entre caminhos que dependem da tarefa você executa.  
  
 **ErrorLevel**  
 Digite a severidade dos problemas de compilação que são relatados como erros. Problemas com níveis de severidade menor ou igual ao valor de **ErrorLevel** são relatados como erros; caso contrário, os problemas são relatados como avisos. Qualquer erro causará falha na tarefa de compilação. Os níveis de severidade válidos são de 0 a 4, inclusive. O valor padrão é 2.  
  
 **StartItem**  
 Selecione o relatório exibido no navegador da Web depois que o projeto é publicado no servidor de relatório ou na janela de visualização quando o projeto é executado localmente. Um item de inicialização é necessário para configurações que criam, mas não implantam o projeto, e para usar o comando **Debug** (**F5**). Ele é necessário para configurações que implantam o projeto.  
  
 **OverwriteDataSources**  
 Selecione **True** para substituir a fonte de dados no servidor pela fonte de dados no projeto quando os relatórios são publicados. Selecione **False** para deixar a fonte de dados existente no servidor.  
  
 **TargetServerVersion**  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Selecione a versão ou [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou selecione **detectar versão** para determinar automaticamente a versão instalada no servidor identificado pela propriedade **URL TargetServer** . O valor padrão é **SQL Server 2008 R2**.  
  
 **TargetDataSourceFolder**  
 O nome da pasta na qual serão armazenadas as fontes de dados compartilhadas publicadas. Se você não especificar uma pasta, a fonte de dados será publicada na mesma pasta do relatório. Se a pasta não existir no servidor de relatório, o Designer de Relatórios irá criar a pasta quando os relatórios forem publicados.  
  
 Quando publicar em um servidor de relatório executado no modo nativo, especifique o caminho completo da hierarquia de pastas a partir da raiz. Por exemplo, Folder1/Folder2/Folder3.  
  
 Quando publicar em um servidor de relatório executado no modo integrado do SharePoint, use uma URL da biblioteca do SharePoint. Por exemplo, http://*\<ServerName>\</site>*/Documents/MyFolder.  
  
 **TargetReportFolder**  
 O nome da pasta em que serão armazenados os relatórios publicados. Por padrão, corresponde ao nome do projeto de relatório. Se a pasta não existir no servidor de relatório, o Designer de Relatórios irá criar a pasta quando os relatórios forem publicados.  
  
 Quando publicar em um servidor de relatório executado no modo nativo, especifique o caminho completo da hierarquia de pastas a partir da raiz. Se uma pasta estiver dentro de outra pasta, inclua um caminho para ela a partir da raiz (por exemplo, Folder1/Folder2/Folder3).  
  
 Quando publicar em um servidor de relatório executado no modo integrado do SharePoint, use uma URL da biblioteca do SharePoint. Por exemplo, http://*\<nomedoservidor>* / * \<site>*/Documents/MyFolder.  
  
 **TargetServerURL**  
 A URL do servidor de relatório de destino. Antes de publicar um relatório, defina essa propriedade com uma URL de servidor de relatório válida.  
  
 Quando publicar em um servidor de relatório executado no modo nativo, use a URL do diretório virtual do servidor de relatório. Por exemplo, http://\<Server>/ReportServer. Este é o diretório virtual do servidor de relatório e não o Gerenciador de Relatórios. Por padrão, o servidor de relatório é instalado em um diretório virtual denominado "reportserver".  
  
 Quando publicar em um servidor de relatório executado no modo integrado do SharePoint, use uma URL de um site de nível superior ou subsite do SharePoint. Se você não especificar um site, o site padrão de nível superior será usado. Por exemplo, http://\<*ServerName>*, http:// *<ServerName*/\<*site>* ou http://\<*ServerName>* / \< *site>* / \< *subsite>*.  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar relatórios](../publish-reports.md)   
 [Publicar um relatório em uma biblioteca do SharePoint](../reports/publish-a-report-to-a-sharepoint-library.md)   
 [Definir propriedades de implantação &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md)   
 [Ajuda F1 do Designer de Relatórios](report-designer-f1-help.md)  
  
  
