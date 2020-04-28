---
title: Visão geral das extensões de segurança | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- security [Reporting Services], extensions
ms.assetid: 24ccd795-6506-457c-93ac-6a9dd6bb9a46
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1041e484732d53ffebec256f3bdee30681118a0c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176962"
---
# <a name="security-extensions-overview"></a>Visão geral de extensões de segurança
  Uma extensão de segurança do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] habilita a autenticação e a autorização de usuários ou grupos; ou seja, ela permite que diferentes usuários façam logon em um servidor de relatório e, com base em suas identidades, executem diferentes tarefas ou operações. Por padrão, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa uma extensão de autenticação baseada no Windows, que usa protocolos de contas do Windows para verificar as identidades de usuários que afirmam ter contas no sistema. O [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa um sistema de segurança baseado em função para autorizar usuários. O modelo de segurança baseada em função do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] é semelhante aos modelos de segurança baseada em função de outras tecnologias.

 Como extensões de segurança se baseiam em uma API aberta e extensível, você pode criar autenticação nova e extensões de autorização no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. Este é um exemplo de implementação de extensão de segurança típica que usa a autenticação baseada em formulários e a autorização:

 ![Processo de extensão de segurança do Reporting Services](../../media/rosettasecurityextensionflow.gif "Processo de extensão de segurança do Reporting Services")

 Conforme mostrado na ilustração, a autenticação e a autorização ocorrem desta forma:

1.  Um usuário tenta acessar o Gerenciador de Relatórios usando uma URL e é redirecionado para um formulário que coleta credenciais de usuário para o aplicativo cliente.

2.  O usuário submete credenciais ao formulário.

3.  As credenciais de usuário são submetidas ao serviço Web do Reporting Services através do método <xref:ReportService2010.ReportingService2010.LogonUser%2A>.

4.  O serviço Web chama a extensão de segurança fornecida pelo cliente e verifica se há nome e senha do usuário na autoridade de segurança personalizada.

5.  Após a autenticação, o serviço Web cria um tíquete de autenticação (conhecido como "cookie"), gerencia o tíquete e verifica a função do usuário para a página inicial do Gerenciador de Relatórios.

6.  O serviço Web devolve o cookie ao navegador e exibe a interface de usuário apropriada no Gerenciador de Relatórios.

7.  Depois da autenticação do usuário, o navegador faz solicitações ao Gerenciador de Relatórios enquanto transmite o cookie no cabeçalho HTTP. Essas solicitações são uma resposta a ações do usuário dentro do aplicativo Gerenciador de Relatórios.

8.  O cookie é transmitido no cabeçalho HTTP para o serviço Web junto com a operação de usuário solicitada.

9. O cookie é validado; quando ele é válido, o servidor de relatório retorna o descritor de segurança e outras informações sobre a operação solicitada do banco de dados do servidor de relatório.

10. Quando o cookie é válido, o servidor de relatório faz uma chamada à extensão de segurança para verificar se o usuário está autorizado a executar a operação específica.

11. Se o usuário estiver autorizado, o servidor de relatório executará a operação solicitada e retornará o controle ao chamador.

12. Depois da autenticação do usuário, o acesso de URL ao servidor de relatório usa o mesmo cookie. O cookie é transmitido no cabeçalho HTTP.

13. O usuário continua solicitando operações no servidor de relatório até o término da sessão.

## <a name="when-to-implement-a-security-extension"></a>Quando implementar uma extensão de segurança
 É recomendável usar a Autenticação do Windows quando isso é possível. Porém, a autenticação personalizada e a autorização do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] podem ser apropriadas nestes dois casos:

-   Você tem um aplicativo Internet ou extranet que não pode usar contas do Windows.

-   Você tem usuários e funções com definição personalizada e precisa fornecer um esquema de autorização compatível no [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].

## <a name="see-also"></a>Consulte Também
 [Implementando uma extensão de segurança](../security-extension/implementing-a-security-extension.md) [Configurar Report Manager para passar cookies de autenticação personalizados](../../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md)


