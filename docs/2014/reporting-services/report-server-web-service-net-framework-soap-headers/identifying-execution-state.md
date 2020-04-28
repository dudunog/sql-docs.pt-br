---
title: Identificando o estado de execução | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- session states [Reporting Services]
- lifetimes [Reporting Services]
- sessions [Reporting Services]
- SessionHeader SOAP header
ms.assetid: d8143a4b-08a1-4c38-9d00-8e50818ee380
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 63c64ee04bc7ece5af8e4040f7795f6f8fbe1c51
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78172206"
---
# <a name="identifying-execution-state"></a>Identificando o estado de execução
  O HTTP (Hypertext Transfer Protocol) é um protocolo sem-conexão e sem-estado, o que significa que ele não indica automaticamente se diferentes solicitações provêm do mesmo cliente ou até se uma única instância de navegador ainda está visualizando ativamente uma página ou site. As sessões criam uma conexão lógica para manter o estado entre servidor e cliente por meio do HTTP. As informações específicas para o usuário, pertinentes a uma sessão específica, são conhecidas como o estado da sessão.

 O gerenciamento de sessão envolve a correlação de uma solicitação de HTTP com outras solicitações anteriores geradas pela mesma sessão. Sem o gerenciamento de sessão, essas solicitações parecem não relacionadas ao serviço Web do servidor de relatório devido à natureza sem-conexão e sem-estado do protocolo HTTP.

 O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não expõe um conceito holístico de estado de sessão como o que é exposto por meio do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. Entretanto, ao executar relatórios, o servidor de relatório mantém o estado entre as chamadas de método no formulário de uma **execução**. A execução permite que o usuário interaja com o relatório de várias maneiras – incluindo o carregamento do relatório do servidor de relatório, configurando credenciais e parâmetros para o relatório e renderizando o relatório.

 Enquanto eles estão se comunicando com um servidor de relatório, os clientes usam a execução para gerenciar a visualização de relatório e a navegação de usuário para outras páginas de um relatório e para mostrar ou ocultar seções de um relatório. Existe uma execução exclusiva para cada relatório que o aplicativo cliente está executando.

 Em geral, o tempo de vida de uma execução inicia quando um usuário navega até um navegador ou aplicativo cliente e seleciona um relatório para exibição. A execução será descartada após um curto tempo limite após a última solicitação até a execução ter sido recebida (o tempo limite padrão é de 20 minutos).

 A partir de uma perspectiva de serviço Web, o tempo de vida inicia quando os métodos do serviço Web do servidor de relatório <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A>, <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A>ou <xref:ReportExecution2005.ReportExecutionService.Render%2A> são chamados. O aplicativo pode usar outros métodos para manipular a execução ativa (por exemplo, definindo os parâmetros e as fontes de dados de configuração). A execução será descartada após um curto tempo limite após a última solicitação até a execução ter sido recebida (o tempo limite padrão é de 20 minutos).

 Um aplicativo monitora várias execuções ativas entre as chamadas para o serviço Web <xref:ReportExecution2005.ReportExecutionService.Render%2A> e os métodos do <xref:ReportExecution2005.ReportExecutionService.RenderStream%2A> salvando o <xref:ReportExecution2005.ExecutionHeader.ExecutionID%2A>, que é retornado no cabeçalho SOAP do <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> e métodos <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A>.

 O diagrama a seguir mostra o processamento e a renderização do caminho para relatórios.

 ![Caminho de processamento/renderização de relatório](../../../2014/reporting-services/media/rs-render-process-diagram.gif "Caminho de processamento/renderização de relatório")

 Para dar suporte às funções descritas acima, o método Processador SOAP atual foi dividido em vários métodos que abrangem a inicialização da execução, o processamento e as fases de renderização.

 Para renderizar programaticamente um relatório, você deve:

-   Carregue o relatório ou a definição de relatório que usa <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> ou <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A>.

-   Verifique se o relatório precisa de credenciais ou parâmetros verificando os valores do <xref:ReportExecution2005.ExecutionInfo.CredentialsRequired%2A> e as propriedades <xref:ReportExecution2005.ExecutionInfo.ParametersRequired%2A> do objeto <xref:ReportExecution2005.ExecutionInfo> retornado por <xref:ReportExecution2005.ReportExecutionService.LoadReport%2A> ou <xref:ReportExecution2005.ReportExecutionService.LoadReportDefinition%2A>

-   Se necessário, defina as credenciais e/ou parâmetros usando os métodos <xref:ReportExecution2005.ReportExecutionService.SetExecutionCredentials%2A> e <xref:ReportExecution2005.ReportExecutionService.SetExecutionParameters%2A>.

-   Chame o método <xref:ReportExecution2005.ReportExecutionService.Render%2A> para renderizar o relatório.

 Enquanto um relatório estiver na sessão, o relatório subjacente armazenado no banco de dados do servidor de relatório poderá ser alterado. Por exemplo, a definição do relatório poderá ser alterada, o relatório poderá ser excluído ou movido e as permissões de usuário poderão ser alteradas. Se o relatório estiver em uma sessão ativa, ele não será afetado pelas alterações efetuadas no relatório subjacente (isto é, o relatório armazenado no banco de dados do servidor de relatório).

 Você também pode gerenciar uma sessão de relatório usando os comandos de acesso da URL.

## <a name="see-also"></a>Consulte Também
 <xref:ReportExecution2005.ReportExecutionService.Render%2A>[Referência técnica &#40;&#41;SSRS](../../../2014/reporting-services/technical-reference-ssrs.md) [usando cabeçalhos SOAP Reporting Services](../report-server-web-service-net-framework-soap-headers/using-reporting-services-soap-headers.md)


