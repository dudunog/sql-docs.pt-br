---
title: Caixa de diálogo Propriedades do relatório, referências | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10530"
- sql12.rtp.rptdesigner.reportproperties.references.f1
ms.assetid: 4639d368-9918-4bb1-9953-7a724ca78dea
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e57e0eb15c8c0ae7e326927ab14493f21c52cc14
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104302"
---
# <a name="report-properties-dialog-box-references"></a>Caixa de diálogo Propriedades do Relatório, Referências
  Selecione **Referências** na caixa de diálogo **Propriedades do Relatório** para adicionar ou remover as referências para assemblies personalizados ou outros assemblies externos e instâncias de classe personalizada usadas pelas expressões na definição do relatório.  
  
## <a name="options"></a>Opções  
 **Adicionar ou remover assemblies**  
 Lista os assemblies aos quais o relatório faz referência. O assembly deve estar disponível no computador no qual a ferramenta que você usando para criar o relatório está instalada e no servidor de relatório. O nome da referência deve corresponder ao conteúdo de ** \<CodeModule>** marcas no arquivo de linguagem de definição de relatório (. RDL) exatamente.  
  
 **Adicionar**  
 Clique para adicionar um assembly. Clique no botão de reticências (...) para abrir a caixa de diálogo **abrir** e selecione os assemblies necessários para concluir o processamento do relatório e a avaliação da expressão.  
  
 **Delete (excluir)**  
 Para remover uma referência de assembly da lista, selecione o nome do assembly e clique no botão **Remover** .  
  
 **Adicionar ou remover classes**  
 Lista as instâncias de classe usadas pelo relatório. A lista de classe só é usada por membros baseados em instância, não membros estáticos.  
  
 **Adicionar**  
 Clique para adicionar uma referência de classe. Clique no botão de reticências (...) para abrir a caixa de diálogo **abrir** e selecione as classes necessárias para concluir o processamento do relatório e a avaliação da expressão.  
  
 **Delete (excluir)**  
 Para excluir a instância de classe, selecione-a e clique no botão **Remover** .  
  
 **Para cima**  
 Para classes que têm dependências, você pode mover esta referência mais para cima na lista.  
  
 **Para baixo**  
 Para classes que têm dependências, você pode mover esta referência mais para baixo na lista.  
  
## <a name="see-also"></a>Consulte Também  
 [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)   
 [As coleções de variáveis de grupo e de relatório fazem referência &#40;Construtor de Relatórios e SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
