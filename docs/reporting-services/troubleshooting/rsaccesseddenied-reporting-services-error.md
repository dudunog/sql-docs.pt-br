---
title: rsAccessedDenied – erro do Reporting Services | Microsoft Docs
description: "Nesta referência de erro, saiba mais sobre \"rsAccessedDenied\": As permissões concedidas ao usuário 'meudomínio\\minhaConta' são insuficientes para a execução dessa operação."
ms.date: 05/22/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ab443e48037add1cc507b71fe87fe7be7bcb43f9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487233"
---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied – erro do Reporting Services
  O erro do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**rsAccessedDenied** ocorre quando um usuário não tem permissão para realizar uma ação. Por exemplo, o usuário não tem uma atribuição de função que o permita abrir um relatório ou ele não abriu seu navegador com as permissões necessárias.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] &#124; Modo do SharePoint|  
  
- Se o erro tiver ocorrido ao acessar o servidor de relatório diretamente através de uma URL, a exceção será mapeada para um erro HTTP 401.  
  
- Se o erro ocorreu ao usar o portal da Web, a exceção normalmente é mapeada para um erro HTTP 401 ou outra página de erro HTML definida.  
  
- Se ele tiver ocorrido durante uma operação, uma assinatura ou uma entrega agendada, o erro será exibido somente no arquivo de log do servidor de relatório.  
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|**Nome do produto**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**ID do evento**|rsAccessedDenied|  
|**Origem do evento**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|**Componente**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**Texto da mensagem**|As permissões concedidas ao usuário 'meudomínio\minhaConta' são insuficientes para a execução dessa operação. (rsAccessDenied) (ReportingServicesLibrary)|  
  
## <a name="user-action"></a>Ação do usuário  
 A permissão para acessar as operações e o conteúdo do servidor de relatório é concedida através de atribuições de função. Em uma nova instalação, somente administradores locais têm acesso a um servidor de relatório. Para conceder acesso a outros usuários, é necessário que um administrador local crie uma atribuição de função que especifique um usuário de domínio ou uma conta de grupo, uma ou mais funções que definem as tarefas que o usuário pode executar e um escopo (geralmente, a pasta Base ou o nó raiz da hierarquia de pastas do servidor de relatório). Você pode usar o portal da Web para criar atribuições de função. Para saber mais, confira [Atribuições de função](../../reporting-services/security/role-assignments.md).  
  
 Esse erro também é causado pela administração local do servidor de relatório. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
## <a name="see-also"></a>Confira também  
 [Atribuições de função](../../reporting-services/security/role-assignments.md)  
 [Conceder permissões em um servidor de relatório no Modo Nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
 [Funções e permissões &#40;Reporting Services&#41;](../../reporting-services/security/roles-and-permissions-reporting-services.md)  
  