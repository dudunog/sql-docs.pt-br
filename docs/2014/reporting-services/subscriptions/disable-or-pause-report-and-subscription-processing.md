---
title: Pausar o processamento de relatório e assinatura | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- subscriptions [Reporting Services], pausing
- report processing [Reporting Services], pausing
- shared data sources [Reporting Services]
- pausing subscription processing
- pausing report processing
- temporarily stopping report processing
- disabling shared data sources
- roles [Reporting Services], modifying
- shared schedules [Reporting Services], pausing
ms.assetid: 3cf9a240-24cc-46d4-bec6-976f82d8f830
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1607637630c507588602dd7e566917ce1eeb6080
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66100918"
---
# <a name="pause-report-and-subscription-processing"></a>Pausar o processamento de relatório e assinatura
  Você não pode pausar um relatório ou assinatura diretamente. No entanto, é possível interromper o processamento de relatório e assinatura antes do início do processamento ou quando uma conexão de fonte de dados for feita. Você também pode impedir o processamento de um relatório ou assinatura deixando-o inacessível para os usuários.  
  
 As estratégias a seguir podem ser usadas para impedir o processamento temporariamente.  
  
## <a name="modify-role-assignments-to-prevent-access"></a>Modificar atribuições de função para impedir o acesso  
 A melhor maneira de deixar um relatório indisponível é remover temporariamente a atribuição de função que fornece acesso ao relatório. Esta abordagem pode ser usada em todos os relatórios, independentemente de como a conexão de fonte de dados seja feita. Esta abordagem visa apenas o relatório, sem afetar a operação de outros relatórios ou itens.  
  
 Para remover a atribuição de função, abra a página Propriedades de Segurança do relatório no Gerenciador de Relatórios. Se o relatório herda a segurança de um pai, clique em **Editar Segurança de Item** para criar uma política de segurança restritiva que omite as atribuições de função que fornecem amplo acesso (por exemplo, você pode remover uma atribuição de função que fornece acesso a Todos e manter a atribuição de função que fornece acesso a um pequeno grupo de usuários, como Administradores).  
  
## <a name="disable-a-shared-data-source"></a>Desabilitar uma fonte de dados compartilhada  
 Uma vantagem de usar fontes de dados compartilhadas é poder desabilitá-las para impedir a execução de um relatório ou assinatura controlada por dados. Desabilitar uma fonte de dados compartilhada desconecta o relatório de sua fonte externa. Enquanto está desabilitada, a fonte de dados fica indisponível para todos os relatórios e assinaturas que a utilizam. Para desabilitar uma fonte de dados compartilhada, abra a fonte de dados no Gerenciador de Relatórios e desmarque a caixa de seleção **Habilitar esta fonte de dados** .  
  
 Observe que o relatório ainda é carregado mesmo que a fonte de dados não esteja disponível. O relatório não contém dados, mas os usuários com as permissões adequadas podem acessar as páginas de propriedade, as configurações de segurança, o histórico de relatórios e as informações de assinatura associadas ao relatório.  
  
## <a name="pause-a-shared-schedule"></a>Pausar uma agenda compartilhada  
 Se um relatório ou assinatura for executado a partir de uma agenda compartilhada, você pode pausar a agenda para impedir o processamento. Todos os processamentos de relatório e assinatura que são controlados pelo agendamento serão adiados até o agendamento ser retomado. Para obter mais informações, consulte [pausar e retomar agendas compartilhadas](schedules.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Página Propriedades de Segurança, Itens &#40;Gerenciador de Relatórios&#41;](../security-properties-page-items-report-manager.md)  
  
  
