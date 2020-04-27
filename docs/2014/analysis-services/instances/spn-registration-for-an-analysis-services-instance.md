---
title: Registro de SPN para uma instância de Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9e78dc37-a3f0-415d-847c-32fec69efa8c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ee52be5eb8c9110e4486a1fa199e3e00572081f3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079567"
---
# <a name="spn-registration-for-an-analysis-services-instance"></a>SPN registration for an Analysis Services instance
  Um nome de entidade de serviço (SPN) identifica exclusivamente uma instância de serviço em um domínio do Active Directory quando a autenticação Kerberos é usada para autenticar identidades de cliente e de serviço mutuamente. Um SPN é associado à conta de logon na qual a instância do serviço é executada.  
  
 Para aplicativos cliente que se conectam ao Analysis Services através da autenticação Kerberos, as bibliotecas de cliente do Analysis Services criam um SPN usando o nome de host da cadeia de conexão e outras variáveis conhecidas, como a classe de serviço, que são corrigidos em qualquer versão especificada do Analysis Services.  
  
 Para que a autenticação mútua ocorra, os SPNs construídos pelo cliente devem corresponder a um objeto SPN em um controlador de domínio do Active Directory. Isso significa que talvez você precise registrar vários SPNs de uma única instância do Analysis Services para dar conta de todas as situações em que um usuário especificará o nome do host em uma cadeia de conexão. Por exemplo, você provavelmente precisará de dois SPNs para tratar o nome de domínio totalmente qualificado (FQDN) de um servidor e o nome abreviado do computador. Registrar corretamente o SPN do Analysis Services é essencial para uma conexão bem-sucedida. Se o SPN for inexistente, estiver com o formato incorreto ou estiver duplicado, a conexão falhará.  
  
 O registro de SPN é uma tarefa manual executada pelo administrador do Analysis Services. Diferente do mecanismo de banco de dados do SQL Server, o Analysis Services nunca registra o SPN automaticamente durante a inicialização do serviço. O registro manual é necessário quando o Analysis Services é executado na conta virtual padrão, uma conta de usuário de domínio ou em uma conta interna, inclusive um SID por serviço.  
  
 O registro de SPN não será exigido se o serviço for executado em uma conta de serviço gerenciado pré-definido criado por um administrador de domínio. Observe que, dependendo do nível funcional do domínio, o registro de um SPN pode solicitar permissões de administrador de domínio.  
  
> [!TIP]  
>  **O Kerberos Configuration Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for é uma ferramenta de diagnóstico que ajuda a solucionar problemas de conectividade relacionados ao Kerberos com o. [!INCLUDE[msCoName](../../includes/msconame-md.md)] ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Para obter mais informações, consulte [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
> [!TIP]  
>  **O Kerberos Configuration Manager [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for é uma ferramenta de diagnóstico que ajuda a solucionar problemas de conectividade relacionados ao Kerberos com o. [!INCLUDE[msCoName](../../includes/msconame-md.md)] ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Para obter mais informações, consulte [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
 Este tópico contém as seguintes seções:  
  
 [Quando o registro de SPN é necessário](#bkmk_scnearios)  
  
 [Formato do SPN do Analysis Services](#bkmk_SPNSyntax)  
  
 [Registro de SPN de uma conta virtual](#bkmk_virtual)  
  
 [Registro de SPN de uma conta de domínio](#bkmk_domain)  
  
 [Registro de SPN de uma conta interna](#bkmk_builtin)  
  
 [Registro de SPN de uma instância nomeada](#bkmk_spnNamed)  
  
 [Registro de SPN de um cluster SSAS](#bkmk_spnCluster)  
  
 [Registro de SPN das instâncias do SSAS configuradas para acesso HTTP](#bkmk_spnHTTP)  
  
 [Registro de SPN das instâncias do SSAS que realizam a escuta em portas fixas](#bkmk_spnFixedPorts)  
  
##  <a name="when-spn-registration-is-required"></a><a name="bkmk_scnearios"></a>Quando o registro de SPN é necessário  
 Qualquer conexão de cliente que especifica "SSPI = Kerberos" na cadeia de conexão introduzirá os requisitos de registro de SPN para uma instância de Analysis Services.  
  
 O registro de SPN é necessário nas seguintes circunstâncias. Para obter informações mais detalhadas, consulte [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
-   A delegação de identidade é necessária para fluir a identidade de usuário do aplicativo cliente ou serviço da camada intermediária para o Analysis Services. A delegação de identidade é geralmente usada quando as permissões por usuário ou filtros são definidos em objetos específicos.  
  
     Um cenário comum envolvendo a delegação de identidade é configurar serviços de camada intermediária, como os Serviços do Excel ou o Reporting Services, para a delegação restrita com a finalidade de representar uma identidade de usuário ao recuperar dados no Analysis Services. Para dar suporte a esse comportamento, você deve fornecer um SPN do Analysis Services como um serviço de destino ao configurar os Serviços de Excel ou Reporting Services para delegação restrita.  
  
-   O Analysis Services delega uma identidade de usuário ao recuperar dados de um banco de dados relacional do SQL Server para bancos de dados de tabela usando o modo DirectQuery. Esse é o único cenário em que o Analysis Services delegará a identidade de usuário para outro serviço.  
  
##  <a name="spn-format-for-analysis-services"></a><a name="bkmk_SPNSyntax"></a>Formato SPN para Analysis Services  
 Use **setspn** para registrar um SPN. Nos sistemas operacionais mais recentes, o **setspn** é instalado como um utilitário do sistema. Para obter mais informações, consulte [SetSPN](https://technet.microsoft.com/library/cc731241\(WS.10\).aspx).  
  
 A tabela a seguir descreve cada parte de um SPN do Analysis Services.  
  
|Elemento|Descrição|  
|-------------|-----------------|  
|Classe de serviço|O MSOLAPSvc.3 identifica o serviço como uma instância do Analysis Services. O .3 é uma referência à versão do protocolo XMLA sobre TCP/IP usado nas transmissões do Analysis Services. Isso não está relacionado à versão do produto. Sendo assim, o MSOLAPSvc.3 é a classe de serviço correta para o SQL Server 2005, 2008, 2008 R2, 2012 e qualquer versão futura do Analysis Services até que o protocolo seja revisado.|  
|Nome do host|Identifica o computador no qual o serviço está sendo executado. Pode ser um nome de domínio totalmente qualificado ou um nome NetBIOS. Você deve registrar um SPN para ambos.<br /><br /> Ao registrar um SPN para o nome de NetBIOS de um servidor, use `SetupSPN -S` para verificar se há registro duplicado. Não há garantia de que os nomes NetBIOS serão exclusivos em uma floresta e ter um registro SPN duplicado causará falha na conexão.<br /><br /> Para clusters de carga balanceada do Analysis Services, o nome de host deve ser o nome virtual atribuído ao cluster.<br /><br /> Nunca crie um SPN usando o endereço IP. O Kerberos usa os recursos de resolução DNS do domínio. A especificação de um endereço IP fará com que esse recurso seja ignorado.|  
|Número da porta|Embora o número da porta faça parte da sintaxe do SPN, você nunca especifica um número de porta ao registrar um SPN do Analysis Services. O caractere de dois-pontos (:), normalmente usado para fornecer um número de porta na sintaxe padrão do SPN, é usado pelo Analysis Services para especificar o nome da instância. Para uma instância do Analysis Services, a porta será considerada a padrão (TCP 2383) ou uma porta atribuída pelo serviço SQL Server Browser (TCP 2382).|  
|Nome da instância|O Analysis Services é um serviço replicável que pode ser instalado várias vezes no mesmo computador. Cada instância é identificada através do nome da instância.<br /><br /> O nome da instância é prefixado com um caractere de dois-pontos (:). Por exemplo, em um computador host chamado SRV01 e uma instância nomeada SSAS-Tabular, o SPN deve ser SRV01:SSAS-Tabular.<br /><br /> Observe que a sintaxe para especificar uma instância nomeada do Analysis Services será diferente da usada por outras instâncias do SQL Server. Outros serviços usam uma barra invertida (\) para anexar o nome da instância a um SPN.|  
|Conta do serviço|Esta é a conta de inicialização do serviço do Windows **MSSQLServerOLAPService** . Ela pode ser uma conta de usuário de domínio do Windows, uma conta virtual, uma conta de serviço gerenciado (MSA) ou uma conta interna, como um SID por serviço, NetworkService ou LocalSystem. Uma conta de usuário de domínio do Windows pode ser formatada user@domaincomo domínio \ usuário ou.|  
  
##  <a name="spn-registration-for-a-virtual-account"></a><a name="bkmk_virtual"></a>Registro de SPN para uma conta virtual  
 As contas virtuais são o tipo de conta padrão para os serviços do SQL Server. A conta virtual é **NT Service\MSOLAPService** para uma instância padrão e **NT Service\MSOLAP $**\<Instance-Name> para uma instância nomeada.  
  
 Como o nome implica, essas contas não existem no Active Directory. Uma conta virtual existe somente no computador local. Ao conectar a serviços externos, aplicativos ou dispositivos, a conexão é feita usando a conta da máquina local. Por essa razão, um registro de SPN para o Analysis Services executado em uma conta virtual é na verdade um registro de SPN para a conta do computador.  
  
 **Exemplo de sintaxe para uma instância padrão em execução como NT Service\MSOLAPService**  
  
 Esse exemplo mostra a sintaxe **setspn** para a instância padrão do Analysis Services executada na conta virtual padrão. Neste exemplo, o nome do host do computador é **AW-SRV01**. Conforme observado, o registro de SPN deve especificar a *conta do computador* em vez da conta virtual, **NT Service\MSOLAPService**.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
> [!NOTE]  
>  Lembre-se de criar dois registros de SPN, um para o nome de host de NetBIOS e um segundo para um nome de domínio totalmente qualificado do host. Diferentes aplicativos clientes usam convenções de nome de host diferentes ao se conectarem ao Analysis Services. Ter dois registros de SPN garante que as duas versões do nome de host sejam consideradas.  
  
 **Exemplo de sintaxe para uma instância nomeada executada como NT Service\MSOLAP\<$ Instance-Name>**  
  
 Esse exemplo mostra a sintaxe **setspn** para uma instância nomeada executada na conta virtual padrão. Nesse exemplo, o nome do host do computador é **AW-SRV02** e o nome da instância é **AW-FINANCE**. Novamente, é a conta da máquina que é especificada para o SPN, em vez da conta virtual **NT Service\MSOLAP $**\<Instance-Name>.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV02.AdventureWorks.com:AW-FINANCE AW-SRV02  
```  
  
##  <a name="spn-registration-for-a-domain-account"></a><a name="bkmk_domain"></a>Registro de SPN para uma conta de domínio  
 Usar uma conta de domínio para executar como uma instância do Analysis Services é uma prática comum.  
  
 Para as instâncias do Analysis Services que são executadas em uma rede ou cluster com carga balanceada de hardware, uma conta de domínio é necessária, com cada instância no cluster executada na mesma conta de domínio.  
  
 **Exemplo de sintaxe para uma instância padrão em execução como um usuário de domínio**  
  
 Esse exemplo mostra a sintaxe **setspn** para a instância padrão do Analysis Services executada na conta do usuário de domínio, **SSAS-Service**, no domínio AdventureWorks.  
  
```  
Setspn -s msolapsvc.3\AW-SRV01.Adventureworks.com AdventureWorks\SSAS-Service  
```  
  
> [!TIP]  
>  Verifique se o SPN foi criado para o servidor do Analysis Services executando `Setspn -L <domain account>` ou `Setspn -L <machinename>`, dependendo de como o SPN foi registrado. Você deve ver MSOLAPSVC. 3/\<hostname> na lista.  
  
##  <a name="spn-registration-for-a-built-in-account"></a><a name="bkmk_builtin"></a>Registro de SPN para uma conta interna  
 Embora essa prática não seja recomendada, instalações antigas do Analysis Services são muitas vezes configuradas para serem executadas em contas internas como Network Service, Local Service ou Local System.  
  
 **Exemplo de sintaxe para uma instância padrão em execução em uma conta interna**  
  
 O registro de SPN para um serviço que é executado em uma conta interna ou SID por serviço é equivalente à sintaxe do SPN usada para a conta virtual. Em vez do nome da conta, use a conta da máquina:  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="spn-registration-for-a-named-instance"></a><a name="bkmk_spnNamed"></a>Registro de SPN para uma instância nomeada  
 Instâncias nomeadas do Analysis Services usam atribuições de porta dinâmica que são detectadas pelo serviço SQL Server Browser. Ao usar uma instância nomeada, registre um SPN para o serviço SQL Server Browser e a instância nomeada do Analysis Services. Para obter mais informações, consulte [Um SPN para o serviço SQL Server Browser é necessário quando você estabelece uma conexão com uma instância nomeada do SQL Server Analysis Services ou do SQL Server](https://support.microsoft.com/kb/950599).  
  
 **Exemplo de sintaxe de SPN para o serviço Navegador do SQL executado como LocalService**  
  
 A classe de serviço é **MSOLAPDisco.3**. Por padrão, esse serviço é executado como NT AUTHORITY\LocalService, que significa que o registro de SPN é definido para a conta do computador. Nesse exemplo, a conta do computador é **AW-SRV01**, correspondendo ao nome do computador.  
  
```  
Setspn -S MSOLAPDisco.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="spn-registration-for-an-ssas-cluster"></a><a name="bkmk_spnCluster"></a>Registro de SPN para um cluster SSAS  
 Para clusters de failover do Analysis Services, o nome de host deve ser o nome virtual atribuído ao cluster. Esse é o nome de rede do SQL Server, especificado durante a instalação do SQL Server quando você instalou o Analysis Services na parte superior de um WSFC existente. Você pode encontrar esse nome no Active Directory. Você também pode encontrá-lo na guia **Gerenciador de cluster de failover** | **Role** | **recursos** da função. O nome do servidor na guia recursos é o que deve ser usado como o ' nome virtual ' no comando SPN.  
  
 **A sintaxe de SPN para um cluster do Analysis Services**  
  
```  
Setspn -s msolapsvc.3/<virtualname.FQDN > <domain user account>  
```  
  
 Lembre-se de que os nós em um cluster do Analysis Services são necessários para usar a porta padrão (TCP 2383) e a executar na mesma conta de usuário de domínio de modo que cada nó tenha o mesmo SID. Consulte [Como criar clusters de SQL Server Analysis Services](https://msdn.microsoft.com/library/dn736073.aspx) para obter mais informações.  
  
##  <a name="spn-registration-for-ssas-instances-configured-for-http-access"></a><a name="bkmk_spnHTTP"></a>Registro de SPN para instâncias do SSAS configuradas para acesso HTTP  
 Dependendo dos requisitos da solução, talvez você tenha configurado o Analysis Services para acesso HTTP. Se a solução incluir o IIS como um componente de camada intermediária, e a autenticação Kerberos for um requisito de solução, talvez seja necessário registrar manualmente um SPN para o IIS. Para obter mais informações, consulte "definir as configurações no computador que está executando o IIS" em [como configurar SQL Server 2008 Analysis Services e SQL Server 2005 Analysis Services para usar a autenticação Kerberos](https://support.microsoft.com/kb/917409).  
  
 Para fins de registro de SPN da instância do Analysis Services, não há nenhuma diferença entre uma instância configurada para TCP ou HTTP. A conexão ao Analysis Services no IIS, por meio da extensão MSMDPUMP ISAPI, é sempre TCP.  
  
 Isso significa que você pode usar as instruções das seções anteriores para que a instância padrão ou nomeada registre o SPN. Ao especificar o nome do host, não deixe de usar o nome do host especificado no arquivo msmdpump.ini ao configurar o serviço para acesso HTTP.  
  
 Para obter mais informações sobre o acesso HTTP, consulte [Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
##  <a name="spn-registration-for-ssas-instances-listening-on-fixed-ports"></a><a name="bkmk_spnFixedPorts"></a>Registro de SPN para instâncias do SSAS escutando em portas fixas  
 Você não pode especificar um número de porta em um registro de SPN do Analysis Services. Se você tiver instalado o Analysis Services como a instância padrão e tiver configurado esse serviço para escutar em uma porta fixa, configure-o para escutar na porta padrão (TCP 2383). No caso de instâncias nomeadas, use o serviço SQL Server Browser e atribuições de porta dinâmica.  
  
 Uma instância do Analysis Services só pode realizar a escuta em uma única porta. Não há suporte para o uso de várias portas. Para obter mais informações sobre a configuração da porta, consulte [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Autenticação do Microsoft BI e delegação de identidade](https://go.microsoft.com/fwlink/?LinkID=286576)   
 [Autenticação mútua usando Kerberos](https://go.microsoft.com/fwlink/?LinkId=299283)   
 [Como configurar SQL Server 2008 Analysis Services e SQL Server 2005 Analysis Services para usar a autenticação Kerberos](https://support.microsoft.com/kb/917409)   
 [Sintaxe do SetSPN dos SPNs (nomes da entidade de serviço) (SetSPN. exe)](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [Qual SPN eu uso e como ele chega lá?](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [SetSPN](https://technet.microsoft.com/library/cc731241\(WS.10\).aspx)   
 [Guia passo a passo das contas de serviço](https://technet.microsoft.com/library/dd548356\(WS.10\).aspx)   
 [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Como usar os SPNs ao configurar aplicativos Web hospedados no Serviços de Informações da Internet](https://support.microsoft.com/kb/929650)   
 [o que há de novo nas contas de serviço](https://technet.microsoft.com/library/dd367859\(WS.10\).aspx)   
 [Configurar a autenticação Kerberos para produtos do SharePoint 2010 (white paper)](https://technet.microsoft.com/library/ff829837.aspx)  
  
  
