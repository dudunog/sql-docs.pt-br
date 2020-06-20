---
title: Reutilização de objetos do pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- GUID regenerating [Integration Services]
- reusing packages
- templates [Integration Services]
- copying packages
- regenerating package GUID
ms.assetid: 08f723bf-15b5-44bd-9a46-04e8781bfbfb
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 086f3d6808668003fa03d79fcbf2911c18b3c0da
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964556"
---
# <a name="reuse-of-package-objects"></a>Reutilizar objetos de pacote
  Agrupa frequentemente as funcionalidades que você deseja usar. Por exemplo, se você criou um conjunto de tarefas, poderá reutilizar os itens juntos como um grupo ou como um único item, como um gerenciador de conexões que você criou em um projeto diferente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="copy-and-paste"></a>Copiar e colar  
 O [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer oferecem suporte a copiar e colar objetos de pacote, que podem incluir itens do fluxo de controle, itens do fluxo de dados e gerenciadores de conexões. Você pode copiar e colar entre projetos e entre pacotes. Se a solução contiver múltiplos projetos, você poderá copiar entre projetos e os projetos podem ser de tipos diferentes.  
  
 Se uma solução contiver múltiplos pacotes, você poderá copiar e colar entre eles. Os pacotes podem estar nos mesmos projetos ou em projetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] diferentes. Entretanto, objetos de pacote podem ter dependências em outros objetos, sem os quais eles não são válidos. Por exemplo, uma tarefa Executar SQL usa um gerenciador de conexões, que você também deve copiar para que a tarefa funcione. Além disso, alguns objetos de pacote exigem que o pacote já contenha um determinado objeto, e sem esse objeto você não pode colar os objetos copiados com sucesso para um pacote. Por exemplo, você não pode colar um fluxo de dados em um pacote que não tenha, no mínimo, uma tarefa de Fluxo de Dados.  
  
 Você pode descobrir que pode copiar os mesmos pacotes repetidamente. Para evitar o processo de cópia, você pode designar estes pacotes como modelos e usá-los quando criar novos pacotes.  
  
 Quando você copia um objeto de pacote, o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] automaticamente atribui uma nova GUID para a propriedade `ID` do novo objeto e atualiza a propriedade `Name`.  
  
 Você não pode copiar variáveis. Se um objeto como uma tarefa usar variáveis, então você deve recriar as variáveis no pacote de destino. Por outro lado, se você copiar o pacote inteiro, as variáveis no pacote também serão copiadas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Copiar objetos de pacote](../../2014/integration-services/copy-package-objects.md)  
  
-   [Copiar itens do projeto](../../2014/integration-services/copy-project-items.md)  
  
-   [Salvar um pacote como um modelo de pacote](../../2014/integration-services/save-a-package-as-a-package-template.md)  
  
  
