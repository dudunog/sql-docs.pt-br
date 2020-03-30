---
title: Arquivo de configuração ReportingServicesService | Microsoft Docs
ms.date: 05/30/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- traces [Reporting Services]
- Report Server Windows service, ReportingServicesService configuration file
- ReportingServicesService configuration file
ms.assetid: 40f4a401-cb61-4c42-b1ec-01acdacdacd1
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: dfb0f48bb35e6341e2b2a9a72007ef4eb09c2b9b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "66506628"
---
# <a name="reportingservicesservice-configuration-file"></a>arquivo de configuração ReportingServicesService

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)]
  
O arquivo ReportingServicesService.exe.config inclui configurações de rastreamento.  
  
## <a name="file-location"></a>Local do arquivo  
Esse arquivo pode estar localizado em um dos caminhos abaixo:  

``` Paths  
\Reporting Services\Report Server\Bin  
\Program Files\Microsoft SQL Server Reporting Services\SSRS\ReportServer\bin  
```  
 
## <a name="editing-guidelines"></a>Editar diretrizes  
 Você pode modificar este arquivo para renomear o arquivo de log ou aumentar ou diminuir níveis de rastreamento. Não modifique nenhuma outra configuração. Para obter instruções, consulte [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md). Para obter mais informações sobre logs de rastreamento, consulte [Log de rastreamento do serviço Servidor de Relatório](../../reporting-services/report-server/report-server-service-trace-log.md).  
  
## <a name="example-configuration"></a>Configuração de exemplo  
 O exemplo a seguir mostra as configurações e os valores padrão localizados no arquivo ReportingServicesService.exe.config.  
  
```  
<configSections>  
      <section name="RStrace" type="Microsoft.ReportingServices.Diagnostics.RSTraceSectionHandler,Microsoft.ReportingServices.Diagnostics" />  
</configSections>  
\<system.diagnostics>  
      <switches>  
          <add name="DefaultTraceSwitch" value="3" />  
      </switches>  
\</system.diagnostics>  
<RStrace>  
      <add name="FileName" value="ReportServerService_" />  
      <add name="FileSizeLimitMb" value="32" />  
      <add name="KeepFilesForDays" value="14" />  
      <add name="Prefix" value="tid, time" />  
      <add name="TraceListeners" value="debugwindow, file" />  
      <add name="TraceFileMode" value="unique" />  
      <add name="Components" value="all" />  
</RStrace>  
<runtime>  
      <alwaysFlowImpersonationPolicy enabled="true"/>  
      <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">  
             <dependentAssembly>  
                    <assemblyIdentity name="Microsoft.ReportingServices.Interfaces"  
                        publicKeyToken="89845dcd8080cc91"  
                        culture="neutral" />  
                    <bindingRedirect oldVersion="8.0.242.0"  
                                     newVersion="10.0.0.0"/>  
                    <bindingRedirect oldVersion="9.0.242.0"  
                                     newVersion="10.0.0.0"/>  
             </dependentAssembly>  
      </assemblyBinding>  
      <gcServer enabled="true" />  
</runtime>  
```  
  
## <a name="configuration-settings"></a>Definições de configuração  
 A tabela a seguir fornece informações sobre configurações específicas. As configurações são apresentadas na ordem em que aparecem no arquivo de configuração.  
  
|Configuração|DESCRIÇÃO|  
|-------------|-----------------|  
|**RStrace**|Especifica os namespaces usados para erros e rastreamento.|  
|**DefaultTraceSwitch**|Especifica o nível de informações que é relatado no log de rastreamento ReportServerService. Cada nível inclui as informações relatadas por todos os níveis de baixa numeração. A desabilitação do rastreamento não é recomendada. Os valores válidos incluem:<br /><br /> 0 = Desabilita o rastreamento<br /><br /> 1 = Exceções e reinicializações<br /><br /> 2 = Exceções, reinicializações, avisos<br /><br /> 3 = Exceções, reinicializações, avisos, mensagens de status (padrão)<br /><br /> 4 = Modo detalhado|  
|**FileName**|Especifica a primeira parte do nome de arquivo de log. O valor especificado por **Prefix** completa o resto do nome. Por padrão, o nome é ReportServerService_.|  
|**FileSizeLimitMb**|Especifica o limite superior do tamanho do log de rastreamento. O arquivo é medido em megabytes. Os valores válidos são de 0 a um inteiro máximo. O valor padrão é 32.|  
|**KeepFilesForDays**|Especifica o número de dias depois dos quais um arquivo de log de rastreamento será excluído. Os valores válidos são de 0 a um inteiro máximo. O valor padrão é 14.|  
|**Prefix**|Especifica um valor gerado que diferencia uma instância de log de outra. Por padrão, os valores do carimbo de data/hora são adicionados aos nomes de arquivo de log de rastreamento. Esse valor é definido como " tid, time ". Não modifique esta configuração.|  
|**TraceListeners**|Especifica um destino para a saída do conteúdo do log de rastreamento. Você pode especificar vários destinos usando uma vírgula para separar cada um. Os valores válidos incluem:<br /><br /> DebugWindow (padrão)<br /><br /> File (padrão)<br /><br /> StdOut|  
|**TraceFileMode**|Especifica se os logs de rastreamento contêm dados para um período de 24 horas. Um log de rastreamento exclusivo deve existir para cada componente em cada dia. Esse valor é definido como "Unique (default)". Não modifique esse valor.|  
|**Componentes**|Especifica os componentes para os quais são criados logs de rastreamento. O valor padrão é **all**. Outros valores válidos para esta configuração incluem os nomes de componentes internos. Não modifique esse valor.|  
|**Runtime**|Especifica configurações que oferecem suporte para a compatibilidade com versões anteriores. As configurações de runtime são usadas para redirecionar solicitações relacionadas à versão anterior de Microsoft.ReportingServices.Interfaces para a nova versão.<br /><br /> Todas as configurações desta seção são descritas na documentação do produto [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Para obter mais informações, procure “Configurações de esquema de runtime” no site do MSDN ou na documentação do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .|  
  
## <a name="see-also"></a>Confira também  
[Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)  
[Log de rastreamento do serviço Servidor de Relatório](../../reporting-services/report-server/report-server-service-trace-log.md)  
  
