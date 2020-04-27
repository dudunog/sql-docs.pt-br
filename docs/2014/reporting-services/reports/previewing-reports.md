---
title: Visualizar relatórios
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.prod: sql-server-2014
ms.technology: reporting-services
ms.prod_service: reporting-services-native, reporting-services-sharepoint
ms.topic: conceptual
ms.custom: seodec18
ms.date: 12/14/2018
ms.openlocfilehash: 21928cd6637815000983e8a0fe05aa4e77d1c216
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67412978"
---
# <a name="preview-reports-in-sql-server-reporting-services-ssrs"></a>Visualizar relatórios no SSRS (SQL Server Reporting Services)

  Ao criar um relatório, convém visualizá-lo antes da publicação em um ambiente de produção. Há várias formas de se fazer isso: você pode alternar para o modo de Visualização no Designer de Relatórios, usar a janela de visualização do Designer de Relatórios e publicar o relatório em um servidor de relatórios em um ambiente de teste.  
  
> [!NOTE]  
> Quando você visualizar um relatório, seus dados serão armazenados em cache em um arquivo no computador local. Ao visualizar novamente o mesmo relatório usando a mesma consulta, os mesmos parâmetros e as mesmas credenciais, o Designer de Relatórios recuperará a cópia em cache em vez de executar a consulta mais uma vez. O arquivo de dados é salvo como * \<ReportName>*. RDL. Data no mesmo diretório que o arquivo de definição de relatório. Ele não será excluído quando você fechar o Designer de Relatórios.  
  
## <a name="preview-mode"></a>Modo de Visualização

 Você pode visualizar um relatório no Report Designer clicando em **Visualizar**. Isso executará o relatório localmente, usando a mesma funcionalidade de processamento e renderização de relatório do servidor de relatórios. O relatório será exibido como uma imagem interativa: é possível selecionar parâmetros, clicar em links, exibir o mapa do documento e expandir e recolher áreas ocultas do relatório. Também é possível exportar o relatório para qualquer formato de renderização instalado.  
  
## <a name="standalone-preview"></a>Visualização autônoma

 Outra forma de visualizar um relatório é executar seu projeto em uma configuração de depuração, por exemplo, para depurar assemblies personalizados que você criou. Há três maneiras de executar um projeto:  
  
- Clicando em **Iniciar** no menu **depurar** .  
  
- Clicando no botão **Iniciar** na barra de [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ferramentas padrão.  
  
- Pressionando F5.  
  
 Se você usar a configuração de projeto que cria um relatório mas não o implanta, o relatório especificado na propriedade `StartItem` da configuração atual será aberto em outra janela de visualização. A janela de visualização exibirá o relatório da mesma forma e terá a mesma funcionalidade do modo de Visualização.  
  
> [!NOTE]  
> Antes de depurar um relatório, defina um item inicial. Para definir um item de início, em Gerenciador de Soluções, clique com o botão direito do mouse **Properties**no projeto de relatório, `StartItem`clique em Propriedades e, em, selecione o nome do relatório a ser exibido.  
  
 Se quiser visualizar um relatório específico que não é o item inicial do projeto, selecione uma configuração que cria o relatório, mas que não o implanta (por exemplo, a configuração DebugLocal), clique com o botão direito do mouse no relatório e clique em **Executar**. Escolha uma configuração que não implante o relatório, caso contrário, o relatório será publicado no servidor de relatórios em vez de ser exibido localmente na janela de visualização.  
  
## <a name="print-preview"></a>Visualizar Impressão

 Na primeira vez em que você visualizar o relatório em modo de Visualização ou na janela de visualização, a exibição do relatório será similar a um relatório gerado pela extensão de renderização HTML. A visualização não é HTML, mas o layout e a paginação do relatório são semelhantes a uma saída em HTML.  
  
 Você pode alterar a exibição para representar um relatório impresso alternando para o modo Visualizar Impressão. Clique no botão **Visualizar Impressão** na barra de ferramentas de visualização. O relatório será exibido como se tivesse sido impresso. Essa exibição é semelhante à saída produzida pelas extensões de renderização de Imagem e PDF. A visualização de impressão não é um arquivo de imagem ou PDF, mas o layout e a paginação do relatório são semelhantes a uma saída nesses formatos.  
  
## <a name="publish-to-a-test-server"></a>Publicar em um Servidor de Teste

 Também é possível testar os relatórios publicando-os em um servidor de teste. A publicação do relatório em um servidor de teste é igual à publicação em um servidor de produção. Para obter informações sobre como publicar um relatório, consulte [Publicando relatórios em um servidor de relatório](publishing-reports-to-a-report-server.md).  
  
## <a name="next-steps"></a>Próximas etapas

 - [Imprimir relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/print-reports-report-builder-and-ssrs.md)
 - [Imprimir um relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/print-a-report-report-builder-and-ssrs.md)
 - [Publicar Relatórios](../publish-reports.md)
 - [Usando assemblies personalizados com relatórios](../custom-assemblies/using-custom-assemblies-with-reports.md)