---
title: Registrar um SPN (Nome da Entidade de Serviço) para um servidor de relatório | Microsoft Docs
ms.date: 02/12/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: dda91d4f-77cc-4898-ad03-810ece5f8e74
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9bfe7a68dc64d2248b9ff9fc4c0696970f692b60
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77256419"
---
# <a name="register-a-service-principal-name-spn-for-a-report-server"></a>Registrar um SPN (Nome da Entidade de Serviço) para um servidor de relatório
  Se estiver implantando o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em uma rede que use o protocolo Kerberos para autenticação mútua, você deverá criar um SPN (Nome da Entidade de Serviço) para o serviço Servidor de Relatório se configurá-lo para execução como uma conta de usuário do domínio.  
  
## <a name="about-spns"></a>Sobre SPNs  
 Um SPN é um identificador exclusivo para um serviço em uma rede que usa autenticação Kerberos. Ele consiste em uma classe de serviço, um nome do host e, algumas vezes, uma porta. Os SPNs HTTP não exigem uma porta. Em uma rede que usa autenticação Kerberos, deve ser registrado um SPN para o servidor em uma conta interna do computador (como NetworkService ou LocalSystem) ou uma conta de usuário. Os SPNs são automaticamente registrados para contas internas. Entretanto, quando executar um serviço em uma conta de usuário do domínio, você deverá registrar manualmente o SPN para a conta que deseja usar.  
  
 Para criar um SPN, você pode usar o utilitário de linha de comando **SetSPN** . Para saber mais, consulte o seguinte:  
  
-   [Setspn](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)) (https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/cc731241(v=ws.11)).  
  
-   [Sintaxe SetSPN (Setspn.exe) de SPNs (nomes de entidade de serviço)](https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx) (https://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx).  
  
 Você deve ser um administrador de domínio para executar o utilitário no controlador de domínio.  
  
## <a name="syntax"></a>Sintaxe  

Ao manipular SPNs com o setspn, o SPN deve ser inserido no formato correto. O formato de um SPN é `<serviceclass>/host:<por>`. A sintaxe de comando para usar o utilitário SetSPN e criar um SPN para o servidor de relatório se assemelha ao seguinte:  
  
```  
Setspn -s http/<computer-name>.<domain-name>:<port> <domain-user-account>  
```  
  
 **SetSPN** está disponível no Windows Server. O argumento de **-s** adiciona um SPN depois de não validar nenhuma duplicata. **OBSERVAÇÃO: -s** está disponível no Windows Server a partir do Windows Server 2008.  
  
 **HTTP** é a classe de serviço. O serviço Web Servidor de Relatórios é executado em HTTP.SYS. Uma criação por produto de um SPN para HTTP significa que todos os aplicativos Web no mesmo computador que são executados em HTTP.SYS (incluindo aplicativos hospedados no IIS) receberão tíquetes com base na conta de usuário do domínio. Se esses serviços forem executados em uma conta diferente, ocorrerá falha nas solicitações de autenticação. Para evitar esse problema, configure todos os aplicativos HTTP para que sejam executados na mesma conta ou considere a criação de cabeçalhos de host para cada aplicativo e, depois, a criação de SPNs separados para cada cabeçalho de host. Quando você configura cabeçalhos de host, é necessário fazer alterações de DNS, independentemente da configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Os valores especificados para \<*computername*> e \<*domainname*> identificam o endereço de rede exclusivo do computador que hospeda o servidor de relatório. Pode ser um nome de host local ou um nome de domínio totalmente qualificado (FQDN). Se tiver somente um domínio, você poderá omitir \<*domainname*> da linha de comando. \<*domain-user-account*> é a conta de usuário na qual o serviço Servidor de Relatório é executado e na qual o SPN deve ser registrado.  
  
## <a name="register-an-spn-for-domain-user-account"></a>Registrar um SPN para a conta de usuário do domínio  
  
### <a name="to-register-an-spn-for-a-report-server-service-running-as-a-domain-user"></a>Para registrar um SPN para um serviço Servidor de Relatório que esteja em execução como um usuário do domínio  
  
1.  Instale o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e configure o serviço Servidor de Relatório para ser executado como uma conta de usuário do domínio. Observe que os usuários não poderão se conectar ao servidor de relatório até que você conclua as etapas a seguir.  
  
2.  Faça logon no controlador de domínio como administrador de domínio.  
  
3.  Abra uma janela de Prompt de Comando.  
  
4.  Copie o seguinte comando, substituindo os valores de espaço reservado por valores reais que sejam válidos para sua rede:  
  
    ```  
    Setspn -s http/<computer-name>.<domain-name>:<port> <domain-user-account>  
    ```  
  
    Por exemplo: `Setspn -s http/MyReportServer.MyDomain.com:80 MyDomainUser`  
  
5.  Execute o comando.  
  
6.  Abra o arquivo **RsReportServer.config** e localize a seção `<AuthenticationTypes>` .  
  
7.  Adicione `<RSWindowsNegotiate/>` como a primeira entrada desta seção para habilitar o Kerberos.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar uma conta de serviço &#40;SSRS Configuration Manager&#41;](../install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Gerenciar um servidor de relatórios de Modo Nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)  
  
  
