---
title: Ativar eventos do Reporting Services para o log de rastreamento do SharePoint (ULS) | Microsoft Docs
description: Saiba como ativar a gravação de eventos do Reporting Services no log de rastreamento ULS do SharePoint para servidores no Reporting Services no modo do SharePoint.
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: 81110ef6-4289-405c-a931-e7e9f49e69ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7ce362356424cb0fdaf991faa27d90f10ef36899
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98597128"
---
# <a name="turn-on-reporting-services-events-for-the-sharepoint-trace-log-uls"></a>Turn on Reporting Services events for the SharePoint trace log (ULS)

  A partir do [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], os servidores do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no modo do SharePoint podem gravar eventos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no log de rastreamento do ULS (Serviço de Log Unificado do SharePoint). [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] estão disponíveis na página Monitoramento da Administração Central do SharePoint.  
  
 Neste tópico:  
  
-   [Recomendações gerais de log ULS](#bkmk_general)  
  
-   [Para ativar e desativar eventos do Reporting Services na categoria do Reporting Services](#bkmk_turnon)  
  
-   [Configuração recomendada](#bkmk_recommended)  
  
-   [Lendo as entradas de logs](#bkmk_readentries)  
  
-   [Lista de eventos do SQL Server Reporting Services](#bkmk_list)  
  
-   [Exiba um arquivo de log com o PowerShell](#bkmk_powershell)  
  
-   [Local do log de rastreamento](#bkmk_trace)  
  
##  <a name="general-uls-log-recommendations"></a><a name="bkmk_general"></a> Recomendações gerais de log ULS  
 A tabela a seguir lista categorias e níveis de eventos recomendados para monitorar um ambiente do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Quando um evento é registrado em log, cada entrada inclui a hora do registro, o nome do processo e a ID do thread.  
  
|Categoria|Nível|Descrição|  
|--------------|-----------|-----------------|  
|Banco de dados|Detalhado|Registra eventos que envolvem acesso ao banco de dados.|  
|Geral|Detalhado|Registra eventos que envolvem acesso aos seguintes itens:<br /><br /> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Páginas da Web<br /><br /> Manipulador de HTTP do Visualizador de Relatórios<br /><br /> Acesso a relatório (arquivos .rdl)<br /><br /> Fontes de dados (arquivos .rsds)<br /><br /> URLs no site do SharePoint (arquivos .smdl)|  
|Geral do Office Server|Exceção|Registra falhas de logon.|  
|Topologia|Detalhado|Registra informações atuais do usuário.|  
|Partes de Web|Detalhado|Registra em log eventos que envolvem o acesso à Web part do Visualizador de Relatórios.|  
  
##  <a name="to-turn-on-and-off-reporting-services-events-in-the-reporting-services-category"></a><a name="bkmk_turnon"></a> Para ativar e desativar eventos do Reporting Services na categoria do Reporting Services  
  
1.  Na Administração Central do SharePoint  
  
2.  Clique em **Monitoramento**.  
  
3.  Clique em **Configurar Log de Diagnóstico** no grupo **Relatório** .  
  
4.  Localize o **SQL Server Reporting Services** na lista de categorias.  
  
5.  Clique no símbolo de adição (+) para expandir as subcategorias sob **SQL Server Reporting Services**.  
  
6.  Selecione as subcategorias a serem adicionadas ao log de rastreamento.  
  
7.  Na parte inferior da lista de categorias, selecione um nível de evento para o **Evento menos crítico a ser relatado no log de rastreamento**. Selecione **Nenhum** para desabilitar o rastreamento.  
  
> [!NOTE]  
>  A opção **Evento menos crítico a ser relatado no log de eventos** não tem suporte no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. A opção é ignorada.  
  
##  <a name="recommended-configuration"></a><a name="bkmk_recommended"></a> Configuração recomendada  
 As seguintes opções de log são recomendadas como uma configuração padrão:  
  
-   **Redirecionador HTTP**  
  
-   **Proxy de Cliente SOAP**  
  
-   Se ocorrerem problemas com a configuração, adicione **Páginas de Configuração**.  
  
 Você pode revisar todas as configurações de log de diagnóstico do farm atual com o seguinte cmdlet do PowerShell:  
  
```  
Get-SPDiagnosticConfig  
```  
  
##  <a name="reading-the-logs-entries"></a><a name="bkmk_readentries"></a> Lendo as entradas de logs  
 As entradas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no log são formatadas da seguinte maneira:  
  
1.  **Produto: SQL Server Reporting Services**  
  
2.  **Categoria:** Eventos relacionados ao servidor terão os caracteres "Servidor de Relatório" no início do nome. Por exemplo "Runtime de Alerta do Servidor de Relatório". Esses eventos também são registrados em log para os arquivos de log do servidor de relatório.  
  
3.  **Categoria:** Eventos relacionados ou comunicados de um componente front-end da Web não contêm "Servidor de Relatório". Por exemplo "Proxy de Aplicativo de Serviço" Runtime de Alerta do Servidor de Relatório". As entradas de WFE contêm um CorrelationID, mas as entradas de servidor não.  
  
##  <a name="list-of-sql-server-reporting-services-events"></a><a name="bkmk_list"></a> Lista de eventos do SQL Server Reporting Services  
 Esta tabela é uma lista dos eventos na categoria SQL Server Reporting Services:  
  
|Nome de área|Descrição ou entradas de exemplo|  
|---------------|-----------------------------------|  
|Páginas de Configuração||  
|Redirecionador HTTP||  
|Processamento do Modo Local||  
|Renderização no Modo Local||  
|Proxy de Cliente SOAP||  
|Páginas de UI||  
|Power View|Entradas de log que foram gravadas na API **LogClientTraceEvents** . Essas entradas derivam de aplicativos de cliente, incluindo o Power View, um recurso do suplemento do SQL Server Reporting Services.<br /><br /> Todas as entradas de log da API LogClientTraceEvents serão registradas na **Categoria** de "SQL Server Reporting Services" e na **Área** de "Power View".<br /><br /> O conteúdo de entradas registradas com a área de "Power View" é determinado pelo aplicativo cliente.|  
|Runtime de alerta do servidor de relatório||  
|Gerenciador de domínio do aplicativo do servidor de relatório||  
|Resposta em buffer do servidor de relatório||  
|Cache do servidor de relatório||  
|Catálogo do servidor de relatório||  
|Parte do servidor de relatório||  
|Limpeza do servidor de relatório||  
|Gerenciador de configuração do servidor de relatório|Entradas de exemplo:<br /><br /> URL interna do servidor de relatório MediumUsing `https://localhost:80/ReportServer`.<br /><br /> UnexpectedMissing ou configuração ExtendedProtectionLevel inválida|  
|Criptografia do servidor de relatório||  
|Extensão de dados do servidor de relatório||  
|Sondagem de BD do servidor de relatório||  
|Padrão do servidor de relatório||  
|Extensão de email do servidor de relatório||  
|Processador Excel do servidor de relatório||  
|Fábrica de extensão do servidor de relatório||  
|Runtime HTTP do servidor de relatório||  
|Processador de imagens do servidor de relatório||  
|Monitoramento de memória do servidor de relatório||  
|Notificação do servidor de relatório||  
|Processamento do servidor de relatório||  
|Provedor do servidor de relatório||  
|Renderização do servidor de relatório||  
|Visualização de relatório do servidor de relatório||  
|Utilitário de recursos do servidor de relatório|Entradas de exemplo:<br /><br /> Serviços de MediumReporting iniciando o SKU: Avaliação<br /><br /> Cópia de MediumEvaluation: 180 dias restantes|  
|Trabalhos em execução do servidor de relatório||  
|Solicitações em execução do servidor de relatório||  
|Agenda do servidor de relatório||  
|Segurança do servidor de relatório||  
|Controlador de serviço do servidor de relatório||  
|Sessão do servidor de relatório||  
|Assinatura do servidor de relatório||  
|Runtime WCF do servidor de relatório||  
|Servidor Web do servidor de relatório||  
|Proxy de aplicativo de serviço||  
|Serviço compartilhado|Entradas de exemplo:<br /><br /> MediumUpdating ReportingWebServiceApplication<br /><br /> Acesso de MediumGranting a bancos de dados de conteúdo.<br /><br /> Instâncias de MediumProvisioning para ReportingWebServiceApplication<br /><br /> Alteração de conta de serviço MediumProcessing para ReportingWebServiceApplication<br /><br /> Permissões de banco de dados MediumSetting|  
  
##  <a name="view-a-log-file-with-powershell"></a><a name="bkmk_powershell"></a> Exiba um arquivo de log com o PowerShell  
 ![Conteúdo relacionado ao PowerShell](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Conteúdo relacionado ao PowerShell")Você poderá usar o PowerShell para retornar uma lista de eventos relacionados ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de um arquivo de log do ULS. Digite o seguinte comando do SharePoint 2010 Management Shell para retornar uma lista filtrada de linhas do arquivo de log ULS UESQL11SPOINT-20110606-1530.log, que contêm "**sql server reporting services**":  
  
```  
Get-content -path "C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS\UESQL11SPOINT-20110606-1530.log" | select-string "sql server reporting services"  
```  
  
 Também há ferramentas que podem ser baixadas que permitirão a leitura de logs do ULS. Por exemplo, o [SharePoint LogViewer](https://github.com/hasankhan/SharePointLogViewer), disponível no GitHub. 
  
 Para obter mais informações sobre como usar o PowerShell para exibir dados de log, consulte [Exibir logs de diagnóstico (SharePoint Server 2010)](/SharePoint/administration/view-diagnostic-logs)  
  
##  <a name="trace-log-location"></a><a name="bkmk_trace"></a> Local do log de rastreamento  
 Os arquivos de log de rastreamento costumam estar localizados na pasta **c:\Arquivos de Programas\Common files\Microsoft Shared\Web Server Extensions\14\logs** , mas você pode verificar ou alterar o caminho na página **Log de Diagnóstico** da Administração Central do SharePoint.  
  
 Para obter mais informações e as etapas para configurar o log de diagnóstico em um servidor SharePoint na Administração Central do SharePoint 2010, consulte [Configurar definições do log de diagnóstico (Windows SharePoint Services)](/previous-versions/office/sharepoint-2007-products-and-technologies/cc288649(v=office.12)).  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)