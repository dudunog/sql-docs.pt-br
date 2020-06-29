---
title: Editor de loop foreach (página Mapeamentos de variáveis) | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.foreachloopcontainer.mapping.f1
ms.assetid: aa847b87-f391-48a5-9849-eeda2d6b00b9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 043077496e1ec1a1cad147725d7f722364f6a54c
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85425493"
---
# <a name="foreach-loop-editor-variable-mappings-page"></a>Editor de Loop Foreach (página Mapeamentos de Variáveis)
  Use a página **Mapeamentos de Variáveis** da caixa de diálogo **Editor de Loop Foreach** para mapear variáveis para o valor da coleção. O valor da variável é atualizado com os valores da coleção em cada iteração do loop.  
  
 Para saber mais sobre como usar o contêiner do Loop Foreach em um pacote de Serviços de Integração, consulte [Contêiner do Loop Foreach](control-flow/foreach-loop-container.md) . Para saber mais sobre como configurá-lo, consulte [Configurar um contêiner do Loop Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
 O tutorial de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] criação de um pacote ETL simples inclui uma lição que ensina a adicionar e configurar um loop foreach.  
  
## <a name="options"></a>Opções  
 **Variável**  
 Selecione uma variável existente ou clique \<**New variable...**> para criar uma nova variável.  
  
> [!NOTE]  
>  Depois que você mapeia uma variável, uma nova linha é adicionada automaticamente à lista **Variável**.  
  
 **Tópicos relacionados**: [Integration Services &#40;&#41; as variáveis do SSIS](integration-services-ssis-variables.md), [Adicionar variável](../../2014/integration-services/add-variable.md)  
  
 **Índice**  
 Se estiver usando o Enumerador de Item Foreach, especifique o índice da coluna no valor da coleção para mapear para a variável. Em outros tipos de enumerador, o índice é somente leitura.  
  
> [!NOTE]  
>  O índice é baseado em 0.  
  
 **Tópicos relacionados**: [Como fazer loop por meio de arquivos e tabelas do Excel usando um contêiner do Loop Foreach](control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
 **Delete (excluir)**  
 Selecione uma variável e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de loop foreach &#40;página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor de loop foreach &#40;página de coleção&#41;](../../2014/integration-services/foreach-loop-editor-collection-page.md)   
 [Página de expressões](expressions/expressions-page.md)   
 [Contêiner Loop For](control-flow/for-loop-container.md)  
  
  
