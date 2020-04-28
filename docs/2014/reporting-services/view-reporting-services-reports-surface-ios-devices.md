---
title: Exibir relatórios de Reporting Services em dispositivos Microsoft Surface e dispositivos Apple iOS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- iPad
- Safari
- SSRS
- Report Viewer [Reporting Services]
- iOS
ms.assetid: 2124bcf5-d60a-475f-a4ae-de6df44d2860
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5ca879d51f947ec078b3c1b7e14842ea926f0240
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174845"
---
# <a name="view-reporting-services-reports-on-microsoft-surface-devices-and--apple-ios-devices"></a>Exibir relatórios do Reporting Services em dispositivos Microsoft Surface e Apple iOS
  Este artigo descreve os recursos e fluxos de trabalho do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] com suporte par dispositivos Microsoft Surface e dispositivos com Apple iOS 6 e Apple Safari, tal como o iPad.

## <a name="view-and-interact-with-reports"></a>Exibir e interagir com relatórios
 A partir do [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)], o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] oferece suporte à exibição e à interatividade básica com relatórios em dispositivos Microsoft Surface, e em dispositivos com Apple iOS 6 e Apple Safari, como o iPad. Você também pode publicar relatórios usando dispositivos Microsoft Surface.

 ![Área de trabalho do iPad](media/videothumbnail.jpg "Área de trabalho de IPad") Assista a uma demonstração de exibição de relatórios em um iPad.

 Você também pode exibir relatórios do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em um dispositivo Windows Phone 8.

 Para usar os recursos descritos neste tópico, instale um dos seguintes:

-   Para um servidor de relatório de modo nativo, instale o [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] ou posterior.

     [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)]está disponível para download no [centro de download da Microsoft](https://www.microsoft.com/download/details.aspx?id=35575).

-   Para um servidor de relatório do modo do SharePoint, instale o [!INCLUDE[ssSQL11SP1long](../includes/sssql11sp1long-md.md)] ou posterior do suplemento [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] para produtos do SharePoint.

 **Para exibir e interagir com um relatório no dispositivo iPad ou Microsoft Surface**

1.  Você deve ser capaz de se conectar ao servidor de relatório ou ao site do SharePoint onde o relatório reside.

2.  Abra o relatório seguindo um destes procedimentos:

    -   **Início no email:** em um email criado por uma assinatura do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] , toque na URL do relatório. O relatório será aberto no navegador.

    -   **Início a partir do servidor de relatório:** procure o diretório no servidor de relatório do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e toque no nome do relatório para abri-lo.

    -   **Início a partir de uma biblioteca de documentos do SharePoint:** navegue até uma biblioteca de documentos do SharePoint que contenha relatórios do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e toque no nome do relatório. Você pode exibir e interagir com o relatório.

        > [!IMPORTANT]
        >  Para o iPad, certifique-se de que a propriedade de **Navegação Particular** para Safari esteja desativada.

    -   **Web parts de SharePoint:** se a Web Part foi adicionada a uma página do SharePoint, você pode exibir relatórios do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .

3.  No dispositivo Microsoft Surface, você também pode abrir o relatório usando o Gerenciador de Relatórios. Procure o diretório no Gerenciador de Relatórios do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e toque no nome do relatório para abri-lo.

    > [!IMPORTANT]
    >  Não há suporte à exibição de relatórios no Gerenciador de Relatórios em um iPad.

4.  Role e aplique zoom fazendo o seguinte:

    -   Para rolar o relatório, arraste seu dedo na tela (para cima, para baixo, para a esquerda ou para a direita). Este é o gesto de passar o dedo.

    -   Para ampliar, coloque dois dedos na tela e separe-os. Para reduzir, coloque dois dedos na tela e aproxime-os. Este é o gesto de pinçagem.

5.  Navegue e interaja com o relatório fazendo o seguinte:

    -   Reduza e expanda itens de relatório e as linhas e colunas associadas a grupos tocando em (+) para reduzir e (-) para expandir.

    -   Alterne entres as ordens crescente e decrescente para linhas de uma tabela ou para linhas e colunas de uma matriz tocando no botão de classificação. O botão de classificação geralmente é posicionado no cabeçalho da coluna.

    -   Expanda e reduza o painel do parâmetro tocando no botão de seta próximo à parte superior do relatório.

    -   Selecione um valor de parâmetro tocando na caixa ou no controle ao lado do parâmetro. Clique em **Exibir Relatório** para aplicar o valor do parâmetro ao relatório.

    -   Pesquise o conteúdo do relatório clicando na caixa ao lado de **Localizar**, digitando um termo de pesquisa e clicando em **Localizar**.

    -   Navegue pelas páginas do relatório clicando nos botões de navegação ou na caixa de texto ao lado dos botões e digitando o número da página.

    -   Navegue até as URLs clicando nos hiperlinks que foram adicionados aos itens de relatório, como caixas de texto, imagens, gráficos e medidores.

    -   Exporte o relatório tocando no ícone do **Menu suspenso Exportar** e toque em um formato de arquivo.

        -   Se você estiver exibindo o relatório em um dispositivo Microsoft Surface, poderá exportar o relatório para um dos formatos a seguir.

            -   Arquivo XML com dados de relatório

            -   CSV (delimitado por vírgulas)

            -   PDF

            -   MHTML (arquivo da Web)

            -   Excel

            -   TIFF

            -   Word

        -   Se você estiver exibindo o relatório em um iPad, poderá exportar o relatório como um arquivo TIFF ou PDF.

## <a name="authentication"></a>Autenticação
 As autenticações RSWindowsNTLM e RSWindowsBasic funcionam apenas com [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] no modo nativo e iPad.

 Em geral, é recomendado que RSWindowsBasic não seja usado em ambientes que não são HTTPs porque esse tipo de autenticação não garante a confidencialidade das credenciais transmitidas.

 Para obter mais informações sobre RSWindowsNTLM e autenticação RSWindowsBasic, consulte [Authentication with the Report Server](security/authentication-with-the-report-server.md).

## <a name="uploading-reports"></a>Carregando relatórios
 Você poderá publicar relatórios de um dispositivo Microsoft Surface usando um dos métodos a seguir, desde que tenha as permissões apropriadas.

> [!IMPORTANT]
>  Esses métodos não têm suporte no iPad.

-   Carregar um arquivo de definição de relatório (.rdl) em uma biblioteca de documentos do SharePoint abrindo a biblioteca e tocando em **Carregar Documento**.

-   Carregar um arquivo de definição de relatório no banco de dados do servidor de relatórios abrindo o Gerenciador de Relatórios e tocando em **Carregar Arquivo**.

## <a name="additional-information"></a>Informações adicionais
 Para obter mais informações sobre o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] e navegadores com suporte, consulte:

-   [Planejamento para Reporting Services e suporte ao navegador de Power View &#40;Reporting Services 2014&#41;](../../2014/reporting-services/browser-support-for-reporting-services-and-power-view.md)

 Para obter mais informações sobre o Microsoft Business Intelligence e dispositivos móveis, consulte o seguinte:

-   [Visão geral de dispositivos móveis e do SharePoint 2013](https://technet.microsoft.com/library/fp161351\(v=office.15\).aspx) (https://technet.microsoft.com/library/fp161351(v=office.15).aspx).

-   [Navegadores de dispositivos móveis com suporte no SharePoint 2013](https://technet.microsoft.com/library/fp161353\(v=office.15\).aspx) (https://technet.microsoft.com/library/fp161353(v=office.15).aspx).

-   [Exibindo relatórios e scorecards em dispositivos Apple iPad (SharePoint Server 2010)](https://technet.microsoft.com/library/hh697482.aspx) (https://technet.microsoft.com/library/hh697482.aspx).

-   [Exibindo Reporting Services relatórios em um iPad (vídeo)](https://technet.microsoft.com/sqlserver/jj873792.aspx) (https://technet.microsoft.com/sqlserver/jj873792.aspx).

-   [Exibindo relatórios do Reporting Services em um dispositivo Microsoft Surface RT (vídeo)](https://technet.microsoft.com/sqlserver/dn146017)


