---
title: Relatórios, partes de relatório e definições de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- report definitions
- reports
ms.assetid: 2d746550-f8cc-4e97-8a06-d0f03cffc18d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d22c8c22170ecef301eacd553f15c16091c9a6e7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105053"
---
# <a name="reports-report-parts-and-report-definitions-report-builder-and-ssrs"></a>Relatórios, partes de relatório e definições de relatório (Construtor de Relatórios e SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]o usa uma variedade de termos para descrever um relatório em diferentes Estados, incluindo a definição inicial, o relatório publicado e o relatório exibido como ele aparece para o usuário.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-definition-rdl-files"></a>Arquivos de definição de relatório (.rdl)  
 Uma definição de relatório é um arquivo que você cria no Construtor de Relatórios ou no Designer de Relatórios. Ela fornece uma descrição completa das conexões de fonte de dados, das consultas usadas para recuperar dados, das expressões, dos parâmetros, das imagens, das caixas de texto, das tabelas e de todos os outros elementos de tempo de design que podem ser incluídos em um relatório. Embora as definições de relatório possam ser complexas, elas especificam, no mínimo, uma consulta e outros conteúdos do relatório, propriedades de relatório e um layout de relatório.  
  
 As definições de relatório são renderizadas em tempo de execução como um relatório processado. Naquele momento, os dados são recuperados da fonte de dados e formatados de acordo com as instruções na definição de relatório. Uma definição de relatório pode ser executada diretamente de seu computador e salva localmente ou pode ser publicada em um servidor de relatório para que outros possam executá-la também.  
  
 As definições de relatório são gravadas em XML em conformidade com uma gramática XML chamada linguagem RDL. A linguagem RDL descreve os elementos XML, abrangendo todas as possíveis variações que um relatório pode assumir.  
  
## <a name="client-report-definition-rdlc-files"></a>Arquivos de definição de relatório de cliente (.rdlc)  
 O Designer de Relatórios do Visual Studio produz arquivos de definição de relatório de cliente (.rdlc) a serem usados com o controle ReportViewer. Os arquivos .rdlc podem ser convertidos em arquivos .rdl para serem usados com o Designer de Relatórios do Reporting Services.  
  
## <a name="report-part-rsc-files"></a>Arquivos de partes de relatório (.rsc)  
 Uma definição de parte de relatório é um fragmento XML de um arquivo de definição de relatório. Para criar partes de relatório, crie uma definição de relatório e depois selecione itens de relatório no relatório para publicar separadamente como partes de relatório. Partes de relatório incluem regiões de dados, retângulos, além dos itens e imagens contidos neles. Você pode salvar uma parte de relatório com conjuntos de dados dependentes e referências à fonte de dados compartilhada para que ela seja reutilizada em outros relatórios.  
  
 [!INCLUDE[ssRBrptparts](../../includes/ssrbrptparts-md.md)]  
  
## <a name="published-reports"></a>Relatórios publicados  
 Após criar um arquivo .rdl, você poderá salvá-lo localmente ou em uma pasta pessoal (como a pasta Meus Relatórios) no servidor de relatório. Quando o relatório está pronto para verificação por outros, você o publica salvando-o do Construtor de Relatórios em uma pasta pública no servidor de relatório, carregando-o através do Gerenciador de Relatórios ou implantando uma solução de projeto de relatório do Designer de Relatórios. Um relatório publicado é um item que foi armazenado em um banco de dados de servidor de relatório e gerenciado em um servidor de relatório ou site do SharePoint.  
  
 Um relatório publicado é protegido por atribuições de função que usam o modelo de segurança baseada em funções do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Os relatórios publicados são acessados por meio de URLs, de Web Parts do SharePoint ou do Gerenciador de Relatórios. Outra opção é navegar até eles e abri-los no Construtor de Relatórios.  
  
### <a name="report-snapshots"></a>Instantâneos de relatório  
 Um relatório também pode ser publicado como um instantâneo que contém informações de layout e dados do momento em que foi executado inicialmente. Os instantâneos de relatório não são salvos em um formato de renderização específico. Em vez disso, os instantâneos de relatório são renderizados em um formato de exibição final (como HTML) somente quando solicitado por um usuário ou aplicativo. Para obter mais informações, consulte [Localizando e exibindo relatórios no Gerenciador de Relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md).  
  
## <a name="rendered-reports"></a>Relatórios renderizados  
 Um relatório renderizado é um relatório totalmente processado que contém dados e informações de layout em um formato adequado para exibição (como HTML). O relatório não pode ser exibido até ser renderizado em um formato de saída. Siga um destes procedimentos para renderizar um relatório:  
  
-   Crie ou abra um relatório no Construtor de Relatórios ou no Designer de Relatórios e execute-o.  
  
-   Localize e execute um relatório no Gerenciador de Relatórios.  
  
-   Localize e execute um relatório em um site do SharePoint integrado com um servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Assine um relatório, que é entregue em uma caixa de entrada de email ou em um compartilhamento de arquivo em um formato de saída especificado por você.  
  
 Assine um relatório, que é distribuído a uma caixa de entrada de emails ou a um compartilhamento de arquivos em um formato de saída especificado por você. O formato de renderização padrão de um relatório é HTML 4.0. Além do HTML, os relatórios podem ser renderizados em diversos formatos de saída, incluindo Excel, Word, XML, PDF, TIFF e CSV. Assim como os relatórios publicados, os relatórios renderizados não podem ser editados nem salvos em um servidor de relatório. Para obter mais informações, consulte [Exportando relatórios &#40;Construtor de relatórios e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos de criação de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-authoring-concepts-report-builder-and-ssrs.md)   
 [Construtor de Relatórios no SQL Server 2014](../report-builder/report-builder-in-sql-server-2016.md)   
 [Instalar, desinstalar e Construtor de Relatórios suporte](../install-uninstall-and-report-builder-support.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS &#41;](../report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
