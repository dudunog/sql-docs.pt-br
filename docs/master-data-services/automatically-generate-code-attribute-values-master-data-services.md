---
title: Gerar automaticamente valores de atributo de código
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: 19b354ee-2906-4cc7-ba2f-32b4543bddcf
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ab9a9fbaac8875be535354a5f6f9122eb5089a0c
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813716"
---
# <a name="automatically-generate-code-attribute-values-master-data-services"></a>Gerar automaticamente valores de atributo de código (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], gera automaticamente valores para o atributo Code de uma entidade quando você deseja atribuir um inteiro automaticamente ao valor de código toda vez que um novo membro é criado.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   A entidade deve existir. Para obter mais informações, consulte [criar uma entidade &#40;Master Data Services&#41;](../master-data-services/create-an-entity-master-data-services.md).  
  
### <a name="to-automatically-generate-code-values"></a>Para gerar valores de código automaticamente.  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na página **Gerenciar Modelo** , selecione a linha do modelo que contém a entidade que você deseja editar e clique em **Entidades**.  
  
3.  Na página **Gerenciar Entidade** , selecione a linha da entidade para a qual deseja criar códigos e clique em **Editar**.  
  
4.  Marque a caixa de seleção **Criar valores de códigos automaticamente** .  
  
5.  Na caixa **Iniciar com** , digite um número para começar a incrementar. Se os membros já existirem, o Código será definido com base no valor existente mais alto. Por exemplo, se o valor de código existente mais alto for 299, o valor de código do próximo membro será definido como 300.  
  
6.  Clique em **Save** (Salvar).  
  
## <a name="see-also"></a>Consulte Também  
 [Criação de código automática &#40;Master Data Services&#41;](../master-data-services/automatic-code-creation-master-data-services.md)   
 [Gerar automaticamente valores de atributo diferentes de código &#40;Master Data Services&#41;](../master-data-services/automatically-generate-attribute-values-other-than-code-master-data-services.md)  
  
  
