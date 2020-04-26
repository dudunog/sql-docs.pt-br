---
title: Proteger Meus Relatórios | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- denying My Reports folder access
- private folders [Reporting Services]
- user workspace [Reporting Services]
- security [Reporting Services], My Reports folder
- My Reports folder [Reporting Services]
ms.assetid: 3b23a382-13b8-4196-9a93-7fe62d03a63c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 88bceac4d712eb1010e4915e11267b7d2ee258a5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101743"
---
# <a name="secure-my-reports"></a>Proteger Meus Relatórios
  O recurso Meus Relatórios fornece um workspace gerenciado pelo usuário para trabalhar com relatórios. Para funcionar conforme pretendido, a pasta Meus Relatórios requer permissões menos restritivas do que as outras pastas que estão disponíveis para uso geral. Os usuários que têm permissões apenas para exibir e executar relatórios em outras pastas podem precisar de um conjunto maior de permissões para gerenciar suas pastas Meus Relatórios e seu próprio conteúdo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece uma atribuição de função especializada e uma definição de função para essa finalidade.  
  
> [!NOTE]  
>  O recurso Meus Relatórios só está disponível no Gerenciador de Relatórios. Não está disponível no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="role-assignment-for-my-reports"></a>Atribuição de função para Meus Relatórios  
 A atribuição de função para Meus Relatórios tem elementos predefinidos e é criada automaticamente para cada usuário que ativa uma pasta Meus Relatórios. A atribuição automática de segurança feita pelo servidor de relatório é especialmente útil para organizações que usam muito o recurso Meus Relatórios porque os administradores não precisam permitir o acesso para cada usuário dessa funcionalidade.  
  
 Uma atribuição de função de **Meus Relatórios** consiste nos seguintes elementos:  
  
-   A pasta Meus Relatórios do usuário, que está localizada na pasta Pastas dos Usuários\\ *\<username>* \Meus Relatórios.  
  
-   A conta de usuário, que é determinada quando a pasta Meus Relatórios é ativada. Uma pasta é ativada quando o usuário clica em uma pasta Meus Relatórios no Gerenciador de Relatórios ou publica um relatório em uma pasta Meus Relatórios a partir do Designer de Relatórios. Essa pasta também é ativada quando o usuário solicita propriedades no link Meus Relatórios.  
  
-   A definição de função predefinida para Meus Relatórios.  
  
## <a name="role-definition-for-my-reports"></a>Definição de função para Meus Relatórios  
 A definição de função de **Meus Relatórios** inclui tarefas que dão suporte ao gerenciamento de conteúdo de uma pasta Meus Relatórios. A função **Meus Relatórios** tem uma única finalidade. Embora seja possível definir qualquer política de segurança no nível do item para essa pasta, evite fazer isso para minimizar a chance de modificá-la para satisfazer requisitos de outra pasta. A reserva da função **Meus Relatórios** para o recurso Meus Relatórios pode ajudar você a manter uma experiência consistente para os usuários.  
  
 Por padrão, só administradores de servidor de relatório modificam a função **Meus Relatórios** . Você pode personalizar a função **Meus Relatórios** alterando as tarefas que ela contém. Você também pode substituir uma função diferente.  
  
## <a name="denying-access-to-my-reports"></a>Negando o acesso a Meus Relatórios  
 Para impedir que os usuários acessem Meus Relatórios:  
  
-   Desabilite Meus Relatórios na página Configurações de Site. Para obter mais informações, consulte [Habilitar e desabilitar Meus Relatórios](../report-server/enable-and-disable-my-reports.md).  
  
-   Remova todas as tarefas da função **Meus Relatórios** .  
  
 Ao desabilitar Meus Relatórios, o link para uma pasta Meus Relatórios é removido do Gerenciador de Relatórios. A estrutura de pasta subjacente que dá suporte a Meus Relatórios (quer dizer, a pasta Pastas dos Usuários e as subpastas) ainda estará disponível e poderá ser acessada se o usuário souber o caminho da pasta. A remoção de tarefas da função **Meus Relatórios** assegura a negação do acesso.  
  
## <a name="see-also"></a>Consulte Também  
 [Proteger relatórios e recursos](secure-reports-and-resources.md)   
 [Proteger pastas](secure-folders.md)   
 [Conceder permissões em um servidor de relatório no Modo Nativo](granting-permissions-on-a-native-mode-report-server.md)  
  
  
