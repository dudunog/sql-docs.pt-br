---
title: Editor de transformação Agrupamento Difuso (guia Gerenciador de conexões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzygroupingtransformation.connection.f1
helpviewer_keywords:
- Fuzzy Grouping Transformation Editor
ms.assetid: 47b1446d-5331-473c-9cb5-a98b1f55bf5f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 8b06f9202bc158d1f64a11c9814792c7fe63ee9d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966326"
---
# <a name="fuzzy-grouping-transformation-editor-connection-manager-tab"></a>Editor de Transformação Agrupamento Difuso (guia Gerenciador de Conexões)
  Use a guia **Gerenciador de Conexões** da caixa de diálogo **Editor de Transformação Agrupamento Difuso** para selecionar uma conexão existente ou criar uma nova.  
  
> [!NOTE]  
>  O servidor especificado pela conexão deve estar executando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A transformação Agrupamento Difuso cria objetos de dados temporários no tempdb que podem ser tão grandes quanto a entrada completa para a transformação. A execução da transformação emite, em seu decorrer, consultas de servidor contra esses objetos temporários. Isso pode afetar o desempenho global de servidor.  
  
 Para saber mais sobre a transformação Agrupamento Difuso, consulte [Fuzzy Grouping Transformation](data-flow/transformations/fuzzy-grouping-transformation.md).  
  
## <a name="options"></a>Opções  
 **Gerenciador de conexões OLE DB**  
 Selecione um gerenciador de conexões OLE DB existente usando a caixa de listagem ou crie uma nova conexão usando o botão **Novo** .  
  
 **Novo**  
 Crie uma nova conexão usando a caixa de diálogo **Configurar Gerenciador de Conexões OLE DB** .  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Identificar linhas de dados semelhantes por meio da transformação Agrupamento Difuso](data-flow/transformations/identify-similar-data-rows-by-using-the-fuzzy-grouping-transformation.md)  
  
  
