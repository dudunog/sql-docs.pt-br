---
title: Adicionar um hiperlink a uma URL (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d3392c0b-7b62-4d27-bc04-2bd0c5487d08
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6fa7b0d32a62e5e2d729e05c88b892ccaffc0fc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106823"
---
# <a name="add-a-hyperlink-to-a-url-report-builder-and-ssrs"></a>Adicionar um hiperlink a uma URL (Construtor de Relatórios e SSRS)
  É possível adicionar um hiperlink a um item de relatório quando você deseja que os usuários possam clicar em um link de um relatório e abrir um navegador para a URL especificada. Um hiperlink pode ser uma URL estático ou uma expressão que seja avaliada como uma URL. Se você tiver um campo em um banco de dados que contenha URLs, a expressão poderá conter esse campo, resultando em uma lista dinâmica de hiperlinks no relatório. Os hiperlinks podem ser adicionados a caixas de texto, imagens, gráficos e medidores. Certifique-se de que o usuário tenha acesso ao URL fornecido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 Você também pode especificar URLs para relatórios em qualquer servidor de relatórios ao qual você e os usuários tenham permissão para exibir usando solicitações de URL para o servidor de relatório. Por exemplo, você pode especificar um relatório e ocultar o mapa do documento para o usuário quando ele exibir o relatório pela primeira vez. Para obter mais informações, consulte [Acesso à URL &#40;SSRS&#41;](../url-access-ssrs.md) na [documentação do Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Você pode adicionar um hiperlink a uma URL para qualquer item que tenha uma propriedade **Action** , como uma caixa de texto, uma imagem ou uma série calculada em um gráfico. Quando o usuário clicar nesse item de relatório, ocorrerá a ação definida. Para obter mais informações, consulte a [Caixa de diálogo Propriedades de ação &#40;Construtor de Relatórios e SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md) e [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 Para começar a usar rapidamente, consulte [Tutorial: Formatar texto &#40;Construtor de Relatórios&#41;](../tutorial-format-text-report-builder.md).  
  
> [!NOTE]  
>  Links associados a campos de conjuntos de dados podem ser vulneráveis à violação para fins mal-intencionados. Para obter mais informações, consulte [Proteger Relatórios e Recursos](../security/secure-reports-and-resources.md) nos [Manuais Online](https://go.microsoft.com/fwlink/?LinkId=154888) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em msdn.microsoft.com.  
  
### <a name="to-add-a-hyperlink"></a>Para adicionar um hiperlink  
  
1.  No modo de exibição de Design de relatório, clique com o botão direito do mouse na caixa de texto, na imagem ou no gráfico a que você deseja adicionar um link e, em seguida, clique em **Propriedades**.  
  
2.  Na caixa de diálogo Propriedades, clique em **Ação**.  
  
3.  Selecione **Ir para URL**. Aparecerá uma seção adicional na caixa de diálogo para essa opção.  
  
4.  Em **Selecionar URL**, digite ou selecione uma URL ou uma expressão avaliada como uma URL, ou clique na seta suspensa e no nome de um campo que contenha uma URL.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (Opcional) O texto não é formatado automaticamente como um link. Para textos, é recomendável alterar sua cor e seu efeito para indicar que ele é um link. Por exemplo, altere a cor para azul e o efeito para sublinhado na seção **Fonte** da guia Página Inicial da Faixa de Opções.  
  
7.  Para testar o link, clique em **Executar** para visualizar o relatório e, em seguida, no item de relatório no qual você definiu esse link.  
  
## <a name="see-also"></a>Consulte Também  
 [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Criar um mapa de documentos &#40;Construtor de Relatórios e SSRS&#41;](create-a-document-map-report-builder-and-ssrs.md)  
  
  
