---
title: Exportando relatórios (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10437"
ms.assetid: a2bab8c1-505d-4da3-b1db-ea0ae13b2336
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d8b4fe6e791f84f0949b0657b890c79db99dfbf9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107952"
---
# <a name="exporting-reports-report-builder-and-ssrs"></a>Exportando relatórios (Construtor de Relatórios e SSRS)
  Depois que você executar um relatório, poderá exportá-lo para outro formato, como Excel ou PDF, ou exportá-lo gerando um documento do serviço Atom, listando os feeds de dados em conformidade com o Atom disponíveis no relatório.  
  
 Para exportar um relatório, siga este procedimento:  
  
-   Trabalhar com os dados do relatório em outro aplicativo. Por exemplo, você pode exportar seu relatório para o Excel e continuar trabalhando com os dados no Excel.  
  
-   Imprimir o relatório em outro formato. Por exemplo, você pode exportar o relatório para o formato de arquivo PDF e depois imprimir o conteúdo dele.  
  
-   Salvar uma cópia do relatório como outro tipo de arquivo. Por exemplo, você pode exportar um relatório para o Word e salvá-lo, criando uma cópia do relatório.  
  
-   Use os dados do relatório como feeds de dados em aplicativos. Por exemplo, você pode gerar feeds de dados em conformidade com [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Atom que o cliente pode consumir e, em seguida, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]trabalhar com os dados no.  
  
 A opção de exportação está disponível na barra de ferramentas do visualizador de relatórios no Gerenciador de Relatórios, que aparece na parte superior de cada relatório exibido no servidor de relatório, e na faixa de opções no Construtor de Relatórios durante a visualização de um relatório. A opção de feed de dados só está disponível no Gerenciador de Relatórios.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece muitas extensões de renderização, suportando exportações de relatórios para formatos de arquivos comuns. As extensões de renderização oferecem suporte somente a quebras flexíveis (por exemplo, Word ou Excel), quebras da página não flexíveis (por exemplo, PDF ou TIFF) ou somente dados (por exemplo, XML compatível com Atom ou CSV).  
  
 Para começar a exportar relatórios e gerar feeds de dados em conformidade com o Atom por meio de relatórios, consulte [exportar um relatório como outro tipo de arquivo &#40;Construtor de relatórios e ssrs&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md) e [gerar feeds de dados de um relatório &#40;Construtor de Relatórios e SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="rendering-extension-types"></a><a name="RendererTypes"></a>Tipos de extensão de renderização  
 Há três tipos de extensões de renderização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   **Extensões dos processadores de dados** As extensões de renderização de dados eliminam todas as informações de formatação e layout do relatório e exibem apenas os dados. O arquivo resultante pode ser usado para importar os dados brutos do relatório em outro tipo de arquivo, como o Excel, outro banco de dados, uma mensagem de dados XML, ou um aplicativo personalizado. Processadores de dados não oferecem suporte a quebras de páginas.  
  
     As seguintes extensões de renderização de dados são suportadas: CSV, XML e Atom.  
  
-   **Extensões do renderizador de quebra suave de página** As extensões de renderização de quebra suave de página mantêm o layout e a formatação do relatório. O arquivo resultante é otimizado para exibição com base em tela e entrega, como em uma página da Web ou nos controles do **ReportViewer** .  
  
     As extensões de renderização de quebra de página flexível a seguir têm suporte: o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word e arquivo da Web (MHTML).  
  
-   **Extensões de renderização de quebra de página impressa** As extensões do renderizador de quebra de página impressa mantêm o layout e a formatação do relatório. O arquivo resultante é otimizado para uma experiência consistente de impressão, ou para exibir o relatório online em formato de um livro.  
  
     As extensões de renderização de quebra de página não flexível a seguinte têm suporte: TIFF e PDF.  
  
##  <a name="export-formats"></a><a name="ExportFormats"></a>Formatos de exportação  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece extensões de renderização que renderizam relatórios em formatos diferentes. Se você planeja usar este recurso, otimize o design de relatório para seu formato de arquivo escolhido. O tópico sobre cada extensão de renderização fornece informações detalhadas sobre como o relatório é renderizado para aquele formato.  
  
 A tabela a seguir lista os formatos disponíveis.  
  
|Formatar|Tipos de extensão de renderização|Descrição|  
|------------|------------------------------|-----------------|  
|CSV|Dados|A extensão de renderização CSV (Comma-Separated Value) renderiza relatórios como uma representação mesclada dos dados de um relatório padronizado, em formato de texto simples que pode ser facilmente lido e que também permite a troca com vários aplicativos.<br /><br /> Para obter mais informações, consulte [Exportar para um arquivo CSV &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md).|  
|Excel|Quebra de página flexível|A extensão de renderização do Excel renderiza um relatório como um documento do Excel compatível com [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2007-2010, bem como com [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 com o Pacote de Compatibilidade do Microsoft Office para Word, Excel e PowerPoint instalado. O relatório é exportado para uma planilha do Excel com alguns elementos de layout e design originais eliminados. As propriedades do relatório e dos grupos dentro do relatório podem ser definidas para habilitar a nomeação de guias de planilha após exportar para o Excel. A extensão do nome de arquivo dos arquivos gerados por esse renderizador é .xlsx.<br /><br /> Para obter mais informações, consulte [Exportar para Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md).<br /><br /> Observação: a extensão de renderização do Excel 2003 que é renderizada para o [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] formato nativo de 2003 está disponível em alguns cenários de relatório.|  
|Word|Quebra de página flexível|A extensão de renderização do Word renderiza um relatório como um documento do Word compatível com [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2007-2010, bem como com [!INCLUDE[ofprword](../../includes/ofprword-md.md)] 2003 com o Pacote de Compatibilidade do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office para Word, Excel e PowerPoint instalado. Depois que o relatório é exportado para um documento do Word, você pode alterar seu conteúdo e criar relatórios com estilo de documento, como etiquetas de endereçamento, ordens de compra ou cartas modelo. A extensão de nome de arquivo dos arquivos gerados por este processador é .docx.<br /><br /> Para obter mais informações, consulte [Exportar para Microsoft Word &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md).<br /><br /> Observação: a extensão de renderização do Word 2003 que é renderizada para o [!INCLUDE[ofprword](../../includes/ofprword-md.md)] formato nativo de 2003 está disponível em alguns cenários de relatório.|  
|Arquivo da Web|Quebra de página flexível|A extensão de renderização HTML renderiza um relatório no formato HTML. A extensão de renderização também pode produzir páginas HTML totalmente formadas ou fragmentos de HTML a serem inseridos em outras páginas HTML. Todo o HTML é gerado com a codificação UTF-8.<br /><br /> A extensão de renderização HTML é a extensão de renderização padrão para relatórios que são exibidos no Construtor de Relatórios e em um navegador, incluindo quando executados no Gerenciador de Relatórios.<br /><br /> Para obter mais informações, consulte [Renderizando para HTML &#40;Construtor de Relatórios e SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md).|  
|Arquivo do Acrobat (PDF)|Quebra de página não flexível|A extensão de renderização PDF renderiza um relatório para os arquivos que podem ser abertos no Adobe Acrobat e em outros visualizadores em PDF de terceiros que dão suporte ao PDF 1.3. Embora o PDF 1.3 seja compatível com o Adobe Acrobat 4.0 e posterior, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dá suporte ao para o Adobe Acrobat 6 ou posterior. A extensão de renderização não requer que o software Adobe renderize o relatório. Porém, os visualizadores de PDF, como o Adobe Acrobat, são necessários para exibir ou imprimir um relatório em formato PDF.<br /><br /> Para obter mais informações, consulte [Exportar para um arquivo PDF &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md).|  
|Arquivo TIFF|Quebra de página não flexível|A extensão de renderização da Imagem renderiza um relatório para um bitmap ou metarquivo. Por padrão, a extensão de renderização da Imagem produz um arquivo TIFF do relatório, que pode ser exibido em várias páginas. Quando o cliente receber a imagem, ela pode ser exibida em um visualizador de imagem e impressa.<br /><br /> A extensão de renderização de Imagem pode gerar arquivos em qualquer um dos formatos que tenham o suporte do [!INCLUDE[ndptecgdiplus](../../includes/ndptecgdiplus-md.md)]: BMP, EMF, EMFPlus, GIF, JPEG, PNG e TIFF.<br /><br /> Para obter mais informações, consulte [Exportando para um arquivo de imagem &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md).|  
|XML|Dados|A extensão XML de renderização retorna um relatório no formato XML. O esquema para o XML do relatório é específico para este relatório e contém somente dados. As informações de layout não são renderizadas e a paginação não é mantida pela extensão XML de renderização. O XML gerado por esta extensão pode ser importado para um banco de dados, usado como uma mensagem de dados XML ou enviado para um aplicativo personalizado.<br /><br /> Para obter mais informações, consulte [Exportação para um XML &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md).|  
|Atom|Dados|A extensão de renderização do Atom gera feeds de dados compatíveis com o Atom a partir de relatórios. Os feeds de dados são legíveis e intercambiáveis com aplicativos como o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cliente que pode consumir feeds de dados em conformidade com o Atom.<br /><br /> A saída é documento de serviço Atom que lista os feeds de dados disponíveis a partir de um relatório. É criado pelo menos um feed de dados para cada região no relatório. Dependendo do tipo de região de dados e dos dados que a região de dados exibe, vários feeds de dados poderão ser gerados.<br /><br /> Para obter mais informações, consulte [gerando feeds de dados de relatórios &#40;Construtor de relatórios e SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md).|  
  
##  <a name="exporting-a-report"></a><a name="ExportingReport"></a>Exportando um relatório  
 Para exportar um relatório, execute-o no Gerenciador de Relatórios ou no Construtor de Relatórios e, em seguida, selecione um formato na lista suspensa Exportar. Você deverá escolher se deseja salvar ou abrir o arquivo. Se você escolher **Abrir**, o relatório será aberto no aplicativo associado ao formato de renderização que foi escolhido. (Por exemplo, quando você seleciona **Excel** o relatório abre em Excel). Se você escolheu **Salvar**, o relatório será salvo. Por exemplo, se você estiver exportando para o Excel, o relatório será salvo como um arquivo .xls. As associações de arquivo definidas no computador local determinam o aplicativo usado para um determinado formato de renderização. Para obter mais informações, consulte [exportar um relatório como outro tipo de arquivo &#40;Construtor de relatórios e SSRS&#41;](../export-a-report-as-another-file-type-report-builder-and-ssrs.md).  
  
 O servidor de relatório exporta o relatório do jeito que ele está na sessão de usuário atual. Se alguém publicar uma versão atualizada do relatório enquanto você estiver com ele aberto ou enquanto os dados que o relatório exibe são modificados, o relatório exportado não será atualizado.  
  
 Pode ser que a paginação do relatório seja afetada quando você exporta um relatório para outro formato. Ao visualizar um relatório, você está visualizando-o como se estivesse renderizado pela extensão de renderização HTML, que segue as regras de quebra de página flexível. Quando você exporta um relatório para um formato de arquivo diferente, como Adobe Acrobat (PDF), a paginação se baseia no tamanho de página físico que segue regras de quebra de página não flexíveis. As páginas também podem ser separadas por quebra de página lógica que você adiciona a um relatório, mas o comprimento real da página varia com base no tipo de processador usado. Para alterar a paginação de seu relatório, você deve entender o comportamento de paginação da extensão de renderização escolhida. Talvez seja necessário ajustar o design de seu layout de relatório para esta extensão de renderização. Para obter mais informações, consulte [layout de página e renderização &#40;Construtor de relatórios e SSRS&#41;](../report-design/page-layout-and-rendering-report-builder-and-ssrs.md).  
  
##  <a name="generating-data-feeds-from-a-report"></a><a name="GeneratingDataFeedsFromReport"></a>Gerando feeds de dados de um relatório  
 Para gerar feeds de dados de um relatório, execute-o no Gerenciador de Relatórios e clique no ícone **Gerar Feed de dados** na barra de ferramentas do Gerenciador de Relatórios. Você deverá escolher se deseja salvar ou abrir o arquivo. Se você escolheu **Abrir**, o documento de serviço do Atom será aberto no aplicativo associado à extensão do arquivo .atomsvc. Se você escolheu **Salvar**, o documento será salvo como um arquivo .atomsvc. Por padrão, o nome do arquivo é o nome do relatório. Você pode alterar o nome para um que seja mais significativo.  
  
 Salve o documento de serviço do Atom em seu computador. Posteriormente, será possível carregá-lo em um servidor de relatório ou outro servidor para que ele seja disponibilizado ao uso de outras pessoas. Para obter mais informações, consulte [Gerando feeds de dados de relatórios &#40;Construtor de Relatórios e SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md) e [Gerar feeds de dados de um relatório &#40;Construtor de Relatórios e SSRS&#41;](generate-data-feeds-from-a-report-report-builder-and-ssrs.md).  
  
##  <a name="troubleshooting-exported-reports"></a><a name="Troubleshooting"></a>Solucionando problemas de relatórios exportados  
 Às vezes, os relatórios parecem diferente ou não funcionam da maneira desejada depois que você os exporta para um formato diferente. Isso ocorre porque determinas regras e limitações podem se aplicar ao renderizador. É possível resolver muitas limitações, considerando-as durante a criação do relatório. Você talvez precise usar um layout um pouco diferente no relatório, alinhar cuidadosamente itens dentro do relatório, confinar rodapés do relatório a uma única linha de texto e assim por diante.  
  
 Se o seu relatório contiver texto Unicode com números arábicos ou contiver datas em árabe, as datas e os números não serão renderizados corretamente quando você exportar o relatório para qualquer um dos seguintes formatos ou imprimir o relatório.  
  
-   PDF  
  
-   Word  
  
-   Excel  
  
-   Imagem/TIFF  
  
 Se você exportar o relatório para HTML, as datas e os números serão renderizados corretamente.  
  
 Os tópicos sobre renderizadores específicos descrevem como itens de relatório e regiões de dados são renderizados, bem como as limitações e as soluções para cada renderizador.  
  
-   [Exportação para um arquivo CSV &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-a-csv-file-report-builder-and-ssrs.md)  
  
-   [Exportando para o Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-microsoft-excel-report-builder-and-ssrs.md)  
  
-   [Exportando para o Microsoft Word &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-microsoft-word-report-builder-and-ssrs.md)  
  
-   [Renderizando para HTML &#40;Construtor de Relatórios e SSRS&#41;](rendering-to-html-report-builder-and-ssrs.md)  
  
-   [Exportação para um arquivo PDF &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-a-pdf-file-report-builder-and-ssrs.md)  
  
-   [Exportando para um arquivo de imagem &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-an-image-file-report-builder-and-ssrs.md)  
  
-   [Exportação para um XML &#40;Construtor de Relatórios e SSRS&#41;](exporting-to-xml-report-builder-and-ssrs.md)  
  
-   [Gerando feeds de dados de relatórios &#40;Construtor de Relatórios e SSRS&#41;](generating-data-feeds-from-reports-report-builder-and-ssrs.md)  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece recursos adicionais para ajudar a criar relatórios que funcionam bem em outros formatos. Quebras de páginas em regiões de dados Tablix (tabela, matriz e lista), grupos e retângulos dão um melhor controle sobre a paginação de relatórios. As páginas do relatório, delimitadas por quebras de páginas, podem ter nomes de página diferentes e a numeração de páginas redefinida. Usando-se expressões, os nomes e os números de páginas podem ser atualizados dinamicamente quando o relatório é executado. Para obter mais informações, consulte [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../report-design/pagination-in-reporting-services-report-builder-and-ssrs.md).  
  
 Além disso, é possível usar RenderFormat interno global para aplicar condicionalmente layouts de relatório diferentes a renderizadores distintos. Para obter mais informações, consulte [Referências de globais internas e referências de usuários &#40;Construtor de Relatórios e SSRS&#41;](../report-design/built-in-collections-built-in-globals-and-users-references-report-builder.md).  
  
##  <a name="other-ways-of-exporting-reports"></a><a name="OtherWaysExportingReports"></a>Outras maneiras de exportar relatórios  
 A exportação de um relatório é uma tarefa sob demanda que você executa quando o relatório é aberto no Gerenciador de Relatórios ou no Construtor de Relatórios. Se quiser automatizar uma operação de exportação (por exemplo, para exportar um relatório para uma pasta compartilhada como um tipo de arquivo específico em uma agenda recorrente), crie uma assinatura que entregue o relatório para uma pasta compartilhada. Para obter mais informações, consulte [File Share Delivery in Reporting Services](../subscriptions/file-share-delivery-in-reporting-services.md).  
  
 Os relatórios visualizados nas ferramentas para relatórios ou abertos em um aplicativo de navegação como o Gerenciador de Relatórios são sempre renderizados primeiro em HTML. Você não pode especificar uma extensão de renderização diferente como padrão para visualização. Todavia, você pode criar uma assinatura que produz um relatório no formato de renderização desejado para a entrega subsequente a uma caixa de entrada de email ou uma pasta compartilhada. Para obter mais informações, consulte [criar, modificar e excluir assinaturas padrão &#40;Reporting Services no modo nativo&#41;](../subscriptions/create-and-manage-subscriptions-for-native-mode-report-servers.md) e [criar, modificar e excluir uma assinatura controlada por dados](../subscriptions/data-driven-subscriptions.md).  
  
 Você também pode acessar um relatório por uma URL que especifique uma extensão de renderização como um parâmetro de URL e renderizar o relatório diretamente para o formato especificado, sem renderizá-lo primeiro em HTML. Este exemplo renderiza um relatório no formato Excel:  
  
```  
http://<Server Name>/reportserver?/Sales/YearlySalesSummary&rs:Format=Excel&rs:Command=Render  
```  
  
 Para saber mais, confira [Export a Report Using URL Access](../export-a-report-using-url-access.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Controlando quebras de página, cabeçalhos, colunas e linhas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/controlling-page-breaks-headings-columns-and-rows-report-builder-and-ssrs.md)   
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS &#41;](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](print-reports-report-builder-and-ssrs.md)   
 [Salvando relatórios &#40;Construtor de Relatórios&#41;](saving-reports-report-builder.md)  
  
  
