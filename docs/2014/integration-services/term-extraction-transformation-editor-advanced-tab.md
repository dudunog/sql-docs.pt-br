---
title: Editor de transformação Extração de termos (guia Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.termextraction.advanced.f1
helpviewer_keywords:
- Term Extraction Transformation Editor
ms.assetid: 87118281-6e3c-499e-bac4-fa4c24bb12c6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 6c783a06d5d5518639e6368f5c1eb572e60206b5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84962256"
---
# <a name="term-extraction-transformation-editor-advanced-tab"></a>Editor de Transformação Extração de Termos (guia Avançado)
  Use a guia **Avançado** da caixa de diálogo **Editor de Transformação de Extração de Termos** para especificar propriedades de extração, como frequência, comprimento e se devem ser extraídas palavras ou frases.  
  
 Para saber mais sobre a transformação Extração de Termos, consulte [Term Extraction Transformation](data-flow/transformations/term-extraction-transformation.md).  
  
## <a name="options"></a>Opções  
 **Substantivo**  
 Especifique que a transformação só extrai substantivos individuais.  
  
 **Frase de substantivo**  
 Especifique que a transformação só extraia frases substantivadas.  
  
 **Substantivo e frase substantivada**  
 Especifique que a transformação extraia tanto substantivos como frases substantivadas.  
  
 **Frequência**  
 Especifique que a pontuação é a frequência do termo.  
  
 **TFIDF**  
 Especifique que a pontuação é o valor TFIDF do termo. A pontuação TFIDF é o produto da Frequência do Termo e da Frequência de Documento Inversa, definido como: TFIDF de um termo T = (frequência de T) * log ((nºs de linhas na Entrada) / (nº de linhas com T))  
  
 **Limite de frequência**  
 Especifique o número de vezes que uma palavra ou frase deve aparecer antes de ser extraída. O valor padrão é 2.  
  
 **Comprimento máximo do termo**  
 Especifique o comprimento máximo de uma frase em palavras. Esta opção só afeta frases substantivadas. O valor padrão é 12.  
  
 **Usar extração de termos com diferenciação de maiúsculas e minúsculas**  
 Especifique se a extração deve ser feita diferenciando maiúsculas e minúsculas. O padrão é `False`.  
  
 **Configurar Saída de Erro**  
 Use a caixa de diálogo [Configurar Saída de Erro](../../2014/integration-services/configure-error-output.md) para especificar tratamento de erro em linhas que causam erros.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor de transformação Extração de termos &#40;guia extração de termos&#41;](../../2014/integration-services/term-extraction-transformation-editor-term-extraction-tab.md)   
 [Editor de transformação Extração de termos &#40;guia exclusão&#41;](../../2014/integration-services/term-extraction-transformation-editor-exclusion-tab.md)   
 [transformação Pesquisa de Termos](data-flow/transformations/lookup-transformation.md)  
  
  
