---
title: Nova Função de Sistema (Management Studio) | Microsoft Docs
description: Saiba mais sobre a página Nova Função do Sistema do Management Studio, em que você cria uma definição de função no nível do sistema que especifica um conjunto de tarefas que se aplicam a um servidor de relatório como um todo.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.newsystemrole.f1
ms.assetid: 7b4a0b98-975b-478a-8359-7db39ccbb347
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 22c3442e16503fd58f8fcb099018b88ab6bfbf92
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915534"
---
# <a name="new-system-role-management-studio"></a>Nova Função do Sistema (Management Studio)
  Use essa página para criar uma definição de função de nível de sistema. Uma definição de função de sistema especifica um conjunto de tarefas de nível de sistema que se aplica a um servidor de relatório como um todo.  
  
> [!NOTE]  
>  Definições de função só são usadas em um servidor de relatório que executa em modo nativo. Se o servidor de relatório for configurado para integração do SharePoint, essa página não estará disponível.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da definição da função. O nome de definição de função deve ser exclusivo no namespace do servidor de relatório. Um nome deve conter pelo menos um caractere alfanumérico. Também pode conter espaços e alguns símbolos. Não use os seguintes caracteres ao especificar um nome:  
  
 ; ? : \@ & = + , $ / * < >  
  
 " /  
  
 **Descrição**  
 Fornece uma descrição que explica como usar a função e enumera a que a função dá suporte.  
  
 **Tarefa**  
 Selecione as tarefas de nível de sistema que podem ser executadas por essa função. Você não pode criar tarefas novas ou modificar as tarefas existentes compatíveis com o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Você não pode escolher tarefas de nível de item para uma definição de função do sistema.  
  
 **Descrição da tarefa**  
 Exibe uma descrição de tarefa que enumera as operações ou permissões às quais a tarefa dá suporte.  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Definições de função](../../reporting-services/security/role-definitions.md)  
  
  
