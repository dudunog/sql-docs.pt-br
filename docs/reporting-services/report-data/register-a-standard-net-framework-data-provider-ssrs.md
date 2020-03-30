---
title: Registrar um Provedor de Dados padrão do .NET Framework | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], data
- .NET Framework data providers for Reporting Services
- data processing extensions [Reporting Services]
- data providers [Reporting Services]
- data retrieval [Reporting Services]
- Reporting Services, data sources
ms.assetid: d92add64-e93c-4598-8508-55d1bc46acf6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0f9435584579e36e46d55aa6723e0ade60b6642b
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081953"
---
# <a name="register-a-standard-net-framework-data-provider-ssrs"></a>Registrar um provedor de dados padrão do .NET Framework (SSRS)
  Para usar um provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] terceirizado com o objetivo de recuperar dados para um conjunto de relatórios do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , é preciso implantar e registrar o assembly do provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] em dois locais: no cliente que está criando o relatório e no servidor de relatório. No cliente que está criando o relatório, você deve registrar o provedor de dados como um tipo de fonte de dados e associá-lo a um designer de consulta. Você pode selecionar esse provedor de dados como um tipo de fonte de dados quando criar um conjunto de dados de relatório. O designer de consulta associado é aberto para ajudá-lo a criar consultas para esse tipo de fonte de dados. No servidor de relatório, é preciso registrar o provedor de dados como um tipo de fonte de dados. Você pode processar os relatórios publicados que recuperam dados a partir de uma fonte de dados usando este provedor de dados.  
  
 Os provedores de dados de terceiros não fornecem necessariamente todas as funções disponíveis nas extensões de processamento de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obter mais informações, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md). Para saber como estender a funcionalidade de um provedor de dados do . provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], confira [Implementando uma extensão de processamento de dados](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md).  
  
 Você precisa ter credenciais de administrador para instalar e registrar provedores de dados.  
  
## <a name="registering-a-net-framework-data-provider-on-the-report-server"></a>Registrando um provedor de dados .NET Framework no Servidor de Relatórios  
 Para processar os relatórios publicados que usam esse provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] no servidor de relatórios, é preciso instalar o assembly no servidor de relatórios. Modifique dois arquivos de configuração. Modifique rsreportserver.config para registrar o provedor de dados. Modifique rssrvpolicy.config para conceder permissões de segurança de acesso do código para o assembly.  
  
#### <a name="to-install-a-data-provider-assembly-on-the-report-server"></a>Para instalar um assembly do provedor de dados no servidor de relatórios  
  
1.  Navegue até o local padrão do diretório \bin no servidor de relatórios no qual deseja usar o provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . A localização padrão do diretório bin do servidor de relatório é *\<drive>* :\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin.  
  
2.  Copie o assembly de seu local de preparação para o diretório \bin do servidor de relatórios. Como alternativa, você pode carregar seu assembly no cache de assembly global (GAC). Para obter mais informações, consulte [Trabalhando com assemblies e cache de assembly global](https://go.microsoft.com/fwlink/?linkid=63912) na documentação do SDK do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] no MSDN.  
  
#### <a name="to-register-a-net-data-provider-on-the-report-server"></a>Para registrar um provedor de dados .NET Framework no servidor de relatórios  
  
1.  Crie um backup do arquivo RSReportServer.config no diretório pai ReportServer do \bin.  
  
2.  Abra o RSReportServer.config. Você pode abrir o arquivo de configuração com o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou um editor de texto simples, como o Bloco de notas.  
  
3.  Localize o elemento **Data** no arquivo RSReportServer.config. Uma entrada para o provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] deve ser criada no seguinte local:  
  
    ```  
    <Extensions>  
       <Data>  
          <Extension Your data provider configuration information goes here />  
       </Data>  
    </Extensions>  
    ```  
  
4.  Adicione uma entrada para o provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
    |Atributo|Descrição|  
    |---------------|-----------------|  
    |**Nome**|Forneça um nome exclusivo para o provedor de dados, como, por exemplo, **MeuProvedorDadosNET**. O comprimento máximo do atributo **Name** é de 255 caracteres. O nome deve ser exclusivo entre todas as entradas dento do elemento **Extension** de um arquivo de configuração. O valor incluído aqui será exibido na lista suspensa dos tipos de fonte de dados quando você criar uma nova fonte de dados.|  
    |**Tipo**|Insira uma lista separada por vírgulas que inclua o namespace totalmente qualificado da classe que implementa a interface <xref:System.Data.IDbConnection> , seguida pelo nome do assembly do provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (sem incluir a extensão de nome de arquivo .dll).|  
  
     Por exemplo, a entrada deve ser semelhante à seguinte para uma DLL implantada no servidor de relatórios do diretório \bin:  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly" />   
    ```  
  
     Se você carregar seu assembly no cache de assembly global (GAC), poderá fornecer as propriedades de nome forte. Por exemplo:  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly,Version=1.0.0.0, Culture=neutral, PublicKeyToken=MyPublicToken"/>  
    ```  
  
#### <a name="to-set-the-code-group-policy-for-a-net-data-provider"></a>Para definir a política do grupo de códigos para um provedor de dados .NET  
  
1.  Faça uma cópia de backup do arquivo rssrvpolicy.config no diretório pai ReportServer do \bin.  
  
2.  Abra o rssrvpolicy.config. Você pode abrir o arquivo de configuração com o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou um editor de texto simples, como o Bloco de notas.  
  
3.  Localize o elemento **CodeGroup** no arquivo rssrvpolicy.config.  
  
4.  Adicione um grupo de códigos para o assembly do provedor de dados que conceda permissão **FullTrust** . O grupo de códigos deve ser semelhante ao seguinte:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="ThisDataProviderCodeGroup"  
       Description="Code group for the .NET data provider">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url=  
    "C:\Program Files\Microsoft SQL Server\MSRS10_50.MSSQLSERVER\Reporting Services\ReportServer\bin\DataProviderAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 A associação da URL é apenas uma das condições de associação que você pode selecionar para o provedor de dados.  
  
### <a name="verifying-the-deployment-and-registration"></a>Verificando a implantação e o registro  
 É possível verificar se o provedor de dados foi implantado com sucesso no servidor de relatório abrindo o portal da Web e verificando se o provedor de dados está incluído na lista de fontes de dados disponíveis. Para obter mais informações sobre o portal da Web e fontes de dados, consulte [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## <a name="registering-a-net-framework-data-provider-on-the-report-designer-client"></a>Registrando um provedor de dados .NET Framework no Cliente do Designer de Relatórios  
 Para criar relatórios que usam esse provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] em uma fonte de dados, é preciso instalar o assembly no computador cliente que estiver executando o Designer de Relatórios. Modifique dois arquivos de configuração. Modifique o arquivo RSReportDesigner.config para registrar o provedor de dados como uma fonte de dados e para usar o designer de consulta genérico. Modifique RSPreviewPolicy.config para conceder permissões de segurança de acesso do código para o assembly do provedor de dados.  
  
#### <a name="to-install-a-data-provider-assembly-on-the-report-designer-client"></a>Para instalar um assembly do provedor de dados no cliente do Designer de Relatórios  
  
1.  Navegue até o local padrão do diretório PrivateAssemblies no cliente do Designer de Relatórios no qual deseja usar o provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . A localização padrão do diretório PrivateAssemblies é *\<drive>* :\Program Files\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies.  
  
2.  Copie o assembly de seu local de preparação para o diretório PrivateAssemblies do cliente do Designer de Relatórios. Como alternativa, você pode carregar seu assembly no cache de assembly global (GAC). Para obter mais informações, consulte [Trabalhando com assemblies e cache de assembly global](https://go.microsoft.com/fwlink/?linkid=63912) na documentação do SDK do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] no MSDN.  
  
#### <a name="to-register-a-net-data-provider-on-the-report-designer-client"></a>Para registrar um provedor de dados .NET no cliente do Designer de Relatórios  
  
1.  Faça uma cópia de backup do arquivo RSReportDesigner.config no diretório PrivateAssemblies.  
  
2.  Abra o arquivo RSReportDesigner.config com o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou um editor de texto simples, como o Bloco de notas.  
  
3.  Localize o elemento **Data** no arquivo RSReportDesigner.config. Uma entrada para o provedor de dados deve ser criada no seguinte local:  
  
    ```  
    <Extensions>  
       <Data>  
          <Extension Your data provider configuration information goes here />  
       </Data>  
    </Extensions>  
    ```  
  
4.  Adicione uma entrada para o provedor de dados.  
  
    |Atributo|Descrição|  
    |---------------|-----------------|  
    |**Nome**|Forneça um nome exclusivo para o provedor de dados, como, por exemplo, **MeuProvedorDadosNET**. O comprimento máximo do atributo **Name** é de 255 caracteres. O nome deve ser exclusivo entre todas as entradas dento do elemento **Extension** de um arquivo de configuração. O valor incluído aqui será exibido na lista suspensa dos tipos de fonte de dados quando você criar uma nova fonte de dados.|  
    |**Tipo**|Insira uma lista separada por vírgulas que inclua o namespace totalmente qualificado da classe que implementa a interface <xref:System.Data.IDbConnection> , seguida pelo nome do assembly do provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] (sem incluir a extensão de nome de arquivo .dll).|  
  
     Por exemplo, a entrada deve ser semelhante à seguinte para uma DLL implantada no diretório PrivateAssemblies do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] :  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly" />   
    ```  
  
     Se você carregar seu assembly no GAC, poderá fornecer as propriedades de nome forte. Por exemplo:  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="CompanyName.ExtensionName.DataProviderConnectionClass, DataProviderAssembly, Version=1.0.0.0, Culture=neutral, PublicKeyToken=MyPublicToken"/>  
    ```  
  
5.  Localize o elemento **Designer** no arquivo RSReportDesigner.config. Uma entrada para o provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] deve ser criada no seguinte local:  
  
    ```  
    <Extensions>  
       <Designer>  
          <Your data provider configuration information goes here>  
       </Designer>  
    </Extensions>  
    ```  
  
6.  Adicione a seguinte entrada ao arquivo RSReportDesigner.config no elemento **Designer** : apenas o atributo **Name** precisará ser substituído pelo nome que você forneceu nas entradas anteriores.  
  
    ```  
    <Extension Name="MyNETDataProvider" Type="Microsoft.ReportingServices.QueryDesigners.GenericQueryDesigner,Microsoft.ReportingServices.QueryDesigners"/>  
    ```  
  
#### <a name="to-set-the-code-group-policy-for-a-net-data-provider-on-the-report-designer-client"></a>Para definir a política do grupo de códigos para um provedor de dados .NET no cliente do Designer de Relatórios  
  
1.  Faça uma cópia de backup do arquivo RSPreviewPolicy.config no diretório PrivateAssemblies.  
  
2.  Abra o arquivo RSPreviewPolicy.config com o [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ou um editor de texto simples, como o Bloco de notas.  
  
3.  Localize o elemento **CodeGroup** no arquivo RSPreviewPolicy.config.  
  
4.  Adicione um grupo de códigos para o assembly do provedor de dados do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que concede a permissão **FullTrust** . O grupo de códigos deve ser semelhante ao seguinte:  
  
    ```  
    <CodeGroup class="UnionCodeGroup"  
       version="1"  
       PermissionSetName="FullTrust"  
       Name="ThisDataProviderCodeGroup"  
       Description="Code group for the .NET data provider">  
          <IMembershipCondition class="UrlMembershipCondition"  
             version="1"  
             Url=  
    " C:\Program Files\Microsoft Visual Studio 9\Common7\IDE\PrivateAssemblies\DataProviderAssembly.dll"  
           />  
    </CodeGroup>  
    ```  
  
 A associação da URL é apenas uma das condições de associação que você pode selecionar para o provedor de dados.  
  
### <a name="verifying-the-deployment-and-registration-on-the-report-designer-client"></a>Verificando a implantação e o registro no Cliente do Designer de Relatórios  
 Antes de verificar a implantação, é preciso fechar todas as instâncias do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] no computador local. Depois de encerrar todas as sessões atuais, você poderá verificar se o provedor de dados foi implantado com êxito ao Designer de Relatórios criando um novo projeto de relatório no [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. O provedor de dados deve ser incluído na lista de tipos de fontes de dados disponíveis quando você criar um novo conjunto de dados para o relatório.  
  
## <a name="platform-considerations"></a>Considerações sobre plataformas  
 Em uma plataforma de 64 bits (x64), o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] é executado no modo WOW de 32 bits. Quando você cria relatórios em uma plataforma x64, é preciso que os provedores de dados de 32 bits estejam instalados no cliente que está criando o relatório para que seja possível visualizá-los. Se publicar o relatório no mesmo sistema, será necessário provedores de dados x64 para exibir o relatório no portal da Web.  
  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Não há suporte para plataformas com base em [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)].  
  
 As extensões de processamento de dados que estão instaladas com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem ser compiladas em modo nativo para cada plataforma e instaladas nos locais corretos. Se você registrar um provedor de dados personalizado ou um provedor de dados padrão do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] , sua compilação deverá ser executada em modo nativo para a plataforma adequada e a instalação deverá ocorrer em locais apropriados. Caso a execução esteja sendo realizada em uma plataforma de 32 bits, o provedor de dados deverá ser compilado para uma plataforma de 32 bits. Caso a execução esteja sendo realizada em uma plataforma de 64 bits, o provedor de dados deverá ser compilado para uma plataforma de 64 bits. Não é permitido usar um provedor de dados de 32 bits com interfaces de 64 bits em uma plataforma de 64 bits. No software de terceiro, procure por informações que possam indicar se o provedor de dados funcionará na plataforma em que você deseja instalá-lo. Para obter mais informações sobre os provedores de dados e o suporte à plataforma, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar e administrar um servidor de relatório &#40;modo nativo do SSRS&#41;](../../reporting-services/report-server/configure-and-administer-a-report-server-ssrs-native-mode.md)   
 [Implementando uma extensão de processamento de dados](../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Segurança de acesso do código no Reporting Services](../../reporting-services/extensions/secure-development/code-access-security-in-reporting-services.md)  
  
  
