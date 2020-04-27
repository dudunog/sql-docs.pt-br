---
title: Metodologias de autenticação com suporte pelo Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: b7aee903-d33a-4c20-86c2-aa013a50949f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a57aff903d41e8bcddef25e21def39a45e33d23f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080338"
---
# <a name="authentication-methodologies-supported-by-analysis-services"></a>Metodologias de autenticação com suporte no Analysis Services
  As conexões de um aplicativo cliente com uma instância do Analysis Services requerem a autenticação do Windows (integrada). Você pode fornecer uma identidade de usuário do Windows usando qualquer um dos seguintes métodos:  
  
-   NTLM  
  
-   Kerberos (consulte [Configurar a delegação restrita do Analysis Services para Kerberos)](configure-analysis-services-for-kerberos-constrained-delegation.md)  
  
-   EffectiveUserName na cadeia de conexão  
  
-   Básica ou Anônima (requer configuração para acesso HTTP)  
  
-   Credenciais armazenadas  
  
 Observe que a autenticação por Declarações não tem suporte. Você não pode usar o token de Declarações do Windows para acessar o Analysis Services. As bibliotecas de cliente do Analysis Services só funcionam com os princípios de segurança do Windows. Se a solução de BI incluir identidades de declarações, você precisará das contas de sombra de identidade do Windows para cada usuário ou usará as credenciais armazenadas para acessar os dados do Analysis Services.  
  
 Para obter mais informações sobre os fluxos de autenticação do BI e do Analysis Services, consulte [Autenticação do Microsoft BI e delegação de identidade](https://go.microsoft.com/fwlink/?LinkID=286576).  
  
##  <a name="understanding-your-authentication-alternatives"></a><a name="bkmk_auth"></a> Noções básicas sobre alternativas de autenticação  
 A conexão a um banco de dados do Analysis Services requer uma identidade de usuário ou grupo do Windows e as permissões associadas. A identidade pode ser um logon com finalidade geral usado por todos que precisam exibir um relatório, mas um cenário mais provável inclui a identidade de usuários individuais.  
  
 Em geral, um modelo tabular ou multidimensional terá diferentes níveis de acesso a dados, por objeto ou dentro dos próprios dados, dependendo de quem está fazendo a solicitação. Para atender a esse requisito, você pode usar autenticação NTLM, Kerberos, EffectiveUserName ou Básica. Todas essas técnicas oferecem um método para passar diferentes identidades de usuário com cada conexão. Entretanto, a maioria dessas opções está sujeita à limitação de um salto único. Somente o Kerberos com delegação permite que a identidade do usuário original flua por várias conexões de computadores até um repositório de dados de back-end em um servidor remoto.  
  
 **NTLM**  
  
 Para as conexões que especificam `SSPI=Negotiate`, o NTLM é o subsistema de autenticação de backup usado quando um controlador de domínio Kerberos não está disponível. Sob NTLM, qualquer usuário ou aplicativo cliente pode acessar um recurso de servidor, desde que a solicitação seja uma conexão direta de um cliente com o servidor, a pessoa que solicita a conexão tenha permissão para o recurso e os computadores cliente e servidor estejam no mesmo domínio.  
  
 Em soluções multicamadas, a restrição de um salto único do NLTM pode ser importante. A identidade do usuário que faz a solicitação pode ser representada em exatamente um servidor remoto, mas não vai além. Se a operação atual que está sendo realizada exigir serviços executados em vários computadores, você deverá configurar a delegação restrita Kerberos para reutilizar o token de segurança em servidores back-end. Como alternativa, você poderá reutilizar credenciais armazenadas ou a autenticação Básica para passar novas informações de identidade em uma conexão de salto único.  
  
 **Autenticação Kerberos e delegação restrita Kerberos**  
  
 A autenticação Kerberos é a base da segurança integrada do Windows em domínios do Active Directory. Assim como o NTLM, a representação com Kerberos é limitada a um único salto, a menos que você habilite a delegação.  
  
 Para dar suporte a conexões de vários saltos, o Kerberos oferece delegação restrita e irrestrita, mas, para a maioria dos cenários, a delegação restrita é considerada uma prática recomendada de segurança. A delegação restrita permite que um serviço passe o token de segurança da identidade do usuário para um serviço de versão anterior designado em um computador remoto. Para os aplicativos de várias camadas, a delegação de uma identidade de usuário de um servidor de aplicativos de camada intermediária para um banco de dados de back-end, como o Analysis Services, é um requisito comum. Por exemplo, um modelo tabular ou multidimensional que retornasse diferentes dados com base na identidade do usuário exigiria delegação de identidade de um serviço de camada intermediária, para evitar que o usuário precisasse reinserir credenciais ou obter credenciais de segurança de alguma outra forma.  
  
 A delegação restrita requer configuração adicional no Active Directory, onde os serviços nas extremidades de envio e recebimento da solicitação são explicitamente autorizados para delegação. Embora haja custos de configuração no futuro, uma vez que o serviço esteja configurado, as atualizações de senha são gerenciadas de modo independente no Active Directory. Você não precisa atualizar informações de conta armazenadas em aplicativos, como faria se usasse a opção de credenciais armazenadas descrita mais adiante.  
  
 Para obter mais informações sobre como configurar o software Analysis Services para delegação restrita, consulte [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
> [!NOTE]  
>  O Windows Server 2012 oferece suporte à delegação restrita entre domínios. Por outro lado, configurar a delegação restrita Kerberos em domínios em níveis funcionais inferiores, como o Windows Server 2008 ou o 2008 R2, requer que os computadores cliente e servidor sejam ambos membros do mesmo domínio.  
  
 **EffectiveUserName**  
  
 EffectiveUserName é uma propriedade de cadeia de conexão usada para passar informações de identidade para o Analysis Services. O PowerPivot para SharePoint a utiliza para registrar a atividade de usuários nos logs de uso. Os Serviços do Excel e os Serviços do PerformancePoint podem usá-lo para recuperar dados usados por pastas de trabalho ou painéis no SharePoint. Ele pode ser usado também em aplicativos ou scripts personalizados que executam operações em uma instância do Analysis Services.  
  
 Para obter mais informações sobre o uso do EffectiveUserName no SharePoint, consulte [Usar o EffectiveUserName do Analysis Services no SharePoint Server 2010](https://go.microsoft.com/fwlink/?LinkId=311905).  
  
 **Autenticação Básica e usuário anônimo**  
  
 A autenticação Básica oferece ainda uma quarta alternativa de conexão com um servidor back-end como um usuário específico. Usando a autenticação Básica, o nome de usuário e a senha do Windows são passados na cadeia de conexão, introduzindo requisitos adicionais de criptografia durante a transmissão para garantir que informações confidenciais sejam protegidas enquanto você está em trânsito. Uma importante vantagem de usar a autenticação Básica é que a solicitação de autenticação pode atravessar limites de domínios.  
  
 Na autenticação Anônima, você pode definir a identidade de usuário anônimo para uma conta de usuário do Windows específica (IUSR_GUEST, por padrão) ou uma identidade de pool de aplicativos. A conta de usuário anônimo será usada na conexão do Analysis Services, e deve ter permissões de acesso a dados na instância do Analysis Services. Quando você usa esse método, somente a identidade de usuário associada à conta Anônima é usada na conexão. Se o seu aplicativo exigir gerenciamento de identidade adicional, você deverá escolher um dos outros métodos, ou o suplemento com uma solução de gerenciamento de identidade que você fornecer.  
  
 As autenticações Básica e Anônima estão disponíveis apenas quando você configura o Analysis Services para acesso HTTP usando o IIS e o arquivo msmdpump.dll para estabelecer a conexão. Para obter mais informações, consulte [Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
 **Credenciais armazenadas**  
  
 A maioria dos serviços de aplicativos de camada intermediária inclui a funcionalidade de armazenamento de um nome de usuário e uma senha usados mais tarde para recuperar dados de um repositório de dados de versão anterior, como o Analysis Services ou o mecanismo relacional do SQL Server. Com isso, as credenciais armazenadas fornecem uma quinta alternativa de recuperação de dados. As limitações desse método incluem sobrecarga de manutenção associada a manter nomes de usuários e senhas atualizados, e o uso de uma única identidade na conexão. Se sua solução exigir a identidade do chamador original, as credenciais armazenadas não serão uma alternativa viável.  
  
 Para obter mais informações sobre credenciais armazenadas, consulte [Criar, modificar e excluir fontes de dados compartilhadas &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md) e [Usar os Serviços do Excel com Serviços de Repositório Seguro no SharePoint Server 2013](https://go.microsoft.com/fwlink/?LinkID=309869).  
  
## <a name="see-also"></a>Consulte Também  
 [Usando a representação com segurança de transporte](https://go.microsoft.com/fwlink/?LinkId=311727)   
 [Configurar o acesso HTTP para Analysis Services em Serviços de Informações da Internet &#40;IIS&#41; 8,0](configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Configurar Analysis Services para delegação restrita de Kerberos](configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Registro de SPN para uma instância de Analysis Services](spn-registration-for-an-analysis-services-instance.md)   
 [Conectar ao Analysis Services](connect-to-analysis-services.md)  
  
  
