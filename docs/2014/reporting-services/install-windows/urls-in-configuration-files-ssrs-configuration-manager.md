---
title: URLs em arquivos de configuração (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL configuration [Reporting Services]
ms.assetid: 4f5e7fe0-b5b1-4665-93d4-80dce12d6b14
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 48deeb3ba6badb1d01b895467f2a8418bdf37ba9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/28/2020
ms.locfileid: "80380707"
---
# <a name="urls-in-configuration-files--ssrs-configuration-manager"></a>URLs em arquivos de configuração (Gerenciador de configurações do SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] armazena configurações de aplicativos em um arquivo RSReportServer.config. Nesse arquivo, há parâmetros de configuração para URLs e reservas de URL. Esses parâmetros de configuração têm propósitos muito diferentes e regras para modificação. Se estiver acostumado a modificar arquivos de configuração para ajustar uma implantação, este tópico pode ajudá-lo a entender como cada configuração de URL é usada.  
  
## <a name="url-settings-in-rsreportserverconfig-file"></a>Configurações de URL no arquivo RSReportServer.config  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] armazena URLs para acesso a aplicativos e relatórios, e para conectar componentes front-end da Web a um servidor de relatório back-end.  
  
#### <a name="urls-for-application-access"></a>URLs para acesso a aplicativos  
 As URLs são usadas para acessar o serviço Web Servidor de Relatórios e o Gerenciador de Relatórios. Para configurar as URLs, você deve usar a ferramenta Configuração do Reporting Services. A ferramenta cria as reservas de URL para cada aplicativo em HTTP.SYS e adiciona entradas para as URLs na seção `URLReservations` de RSReportServer.config.  
  
-   Para exibir as descrições `URLReservations` de cada elemento na seção, consulte [RSReportServer Configuration File](../report-server/rsreportserver-config-configuration-file.md) in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Books Online.  
  
-   Para obter mais informações sobre a `UrlString` sintaxe de apenas o elemento, consulte [Sintaxe de Reserva de URL &#40;SSRS Configuration Manager&#41;](url-reservation-syntax-ssrs-configuration-manager.md).  
  
-   Para obter instruções sobre como configurar uma URL para acesso do aplicativo, veja [Configurar uma URL &#40;SSRS Configuration Manager&#41;](configure-a-url-ssrs-configuration-manager.md).  
  
#### <a name="urls-for-report-access"></a>URLs para acesso a relatórios  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui uma extensão de entrega de email do servidor de relatório que você pode usar para enviar links de relatórios ou anexos. Um link de relatório é construído quando o relatório é entregue. A extensão de entrega de email do servidor de relatório usa a configuração `UrlRoot` no arquivo de configuração para criar o link. `UrlRoot` também é usada para resolver links em um relatório renderizado que é gerado por processamento de relatório autônomo.  
  
 `UrlRoot` será especificada automaticamente no arquivo RSReportServer.config quando você configurar as URLs para acesso a aplicativos. Se você modificar esse valor no arquivo de configuração, deverá especificar um endereço de URL válido para um serviço Web Servidor de Relatórios que esteja conectado a um banco de dados do servidor de relatório que contém os relatórios que você deseja entregar. Você pode especificar apenas uma `UrlRoot` para uma única instância do servidor de relatório; apenas uma entrada `UrlRoot` pode existir no arquivo RSReportServer.config para qualquer instância específica do servidor de relatório. Se você tiver várias URLs reservadas para o serviço Web Servidor de Relatórios, deverá escolher um dos valores disponíveis para `UrlRoot`.  
  
 Na maioria dos casos, não é necessário modificar `UrlRoot`. No entanto, se o servidor de relatórios for acessado através de uma URL totalmente qualificada e você não configurar uma URL que usa um cabeçalho de host para o nome do site totalmente qualificado, você deve editar o RSReportServer.config manualmente para definir a URL do `UrlRoot` servidor de relatório totalmente qualificada que será usada para renderizar o relatório (por exemplo, `https://www.adventure-works.com/mywebapp/reportserver`).  
  
#### <a name="urls-connecting-report-manager-and-web-parts-to-the-report-server-web-service"></a>URLs conectando o Gerenciador de Relatórios e Web Parts ao serviço Web Servidor de Relatórios  
 O Gerenciador de Relatórios e o SharePoint 2.0 Web Parts for Reporting Services são componentes front-end da Web que se conectam a um servidor de relatório. As URLs usadas para conexão a um servidor de relatório back-end incluem o seguinte:  
  
-   `ReportServerUrl` (usada pelo Gerenciador de Relatórios)  
  
-   `ReportServerExternalUrl` (usada pelo Web Parts)  
  
> [!NOTE]  
>  As versões anteriores do Reporting Services incluíam o elemento `ReportServerVirtualDirectory`. Este valor está obsoleto em [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e nas versões posteriores. Se você atualizou uma instalação existente e estiver usando um arquivo de configuração que contenha essa configuração, o servidor de relatório não lerá mais esse valor.  
  
 A tabela a seguir fornece um resumo de todas as URLs que podem ser especificadas em um arquivo de configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
|Configuração|Uso|Descrição|  
|-------------|-----------|-----------------|  
|`ReportServerUrl`|Opcional. Este elemento não será incluído no arquivo RSReportServer.config a menos que você mesmo o adicione. Só defina este elemento se você estiver configurando um dos seguintes cenários:<br /><br /> O Gerenciador de Relatórios fornece acesso front-end da Web a um serviço Web Servidor de Relatórios que é executado em um computador diferente ou em uma instância diferente no mesmo computador.<br /><br /> Quando existem várias URLs para um servidor de relatório e você deseja que o Gerenciador de Relatórios use uma URL específica.<br /><br /> Você tem uma URL específica do servidor de relatório pela qual você deseja que todas as conexões do Gerenciador de Relatórios use.<br /><br /> Por exemplo, você poderia habilitar o acesso do Gerenciador de Relatórios a todos os computadores na rede e ainda requerer que o Gerenciador de Relatórios conecte-se ao servidor de relatório por meio de uma conexão local. Neste caso, você pode `ReportServerUrl` configurarhttp://localhost/reportserverpara " ".<br /><br /> <br /><br /> Para obter instruções sobre como implementar esses cenários, consulte [Configurar o Gerenciador de relatórios &#40;modo nativo&#41;](../report-server/configure-web-portal.md) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Livros Online.|Esse valor especifica uma URL para o serviço Web Servidor de Relatórios. Esse valor é lido pelo aplicativo Gerenciador de Relatórios durante a inicialização. Se esse valor for definido, o Gerenciador de Relatórios será conectado ao servidor de relatório que está especificado na URL.<br /><br /> Por padrão, o Gerenciador de Relatórios fornece acesso front-end da Web ao serviço Web Servidor de Relatórios que é executado na mesma instância do servidor de relatório que o Gerenciador de Relatórios. Entretanto, para usar o Gerenciador de Relatórios com um serviço Web Servidor de Relatórios que faz parte de outra instância ou é executado em uma instância em um computador diferente, é possível configurar essa URL de maneira a instruir o Gerenciador de Relatórios a conectar-se ao serviço Web Servidor de Relatórios externo.<br /><br /> Se um certificado SSL (Secure Sockets Layer) estiver instalado no servidor de relatório ao qual você está se conectando, o valor de `ReportServerUrl` deverá ser o nome do servidor que está registrado para esse certificado. Se você obtiver o erro "A conexão subjacente foi fechada: Não foi possível estabelecer uma relação de confiança para o canal de segurança SSL/TLS", defina `ReportServerUrl` como o nome de domínio totalmente qualificado do servidor para o qual o certificado SSL foi emitido. Por exemplo, se o certificado estiver registrado em **https:\//adventure-works.com.onlinesales,** o URL do servidor de relatórios seria **https:\//adventure-works.com.onlinesales/reportserver**.|  
|`ReportServerExternalUrl`|Opcional. Este elemento não será incluído no arquivo RSReportServer.config a menos que você mesmo o adicione.<br /><br /> Defina este elemento apenas se você estiver usando o SharePoint 2.0 Web Parts e deseja que os usuários possam recuperar um relatório e abri-lo em uma nova janela do navegador.<br /><br /> Adicione `ReportServerExternalUrl` <> `ReportServerUrl` abaixo do elemento> <e, em seguida, defina-o como um nome de servidor de relatório totalmente qualificado que resolve uma instância de servidor de relatório quando acessado em uma janela de navegador separada. Não exclua `ReportServerUrl` <>.<br /><br /> O exemplo a seguir ilustra a sintaxe:<br /><br /> `<ReportServerExternalUrl>http://myserver/reportserver</ReportServerExternalUrl>`|Este valor é usado pelo SharePoint 2.0 Web Parts.<br /><br /> Em versões anteriores, era recomendado configurar esse valor para implantar o Construtor de Relatórios em um servidor de relatório na Internet. Esse é um cenário de implantação não testado. Se você usava essa configuração para oferecer suporte de acesso à Internet ao Construtor de Relatórios, deverá considerar uma estratégia alternativa.|  
  
## <a name="see-also"></a>Consulte também  
 [Configurar URLs do servidor de relatório&#40;gerenciador de configuração SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](configure-a-url-ssrs-configuration-manager.md)  
  
  
