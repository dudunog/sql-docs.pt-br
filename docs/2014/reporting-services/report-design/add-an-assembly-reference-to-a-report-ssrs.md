---
title: Adicionar uma referência de assembly a um relatório (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- code [Reporting Services]
- custom assemblies [Reporting Services], referencing
- custom code [Reporting Services]
- adding assembly references
- assemblies [Reporting Services], references
ms.assetid: 0a03939e-48ce-4c30-b227-98533f2e0ccb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 23dda0c65589e55849f906c621e42ce70f0d7ab5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106754"
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>Adicionar uma referência de assembly a um relatório (SSRS)
  Quando você insere o código personalizado que contém referências a classes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que não estão no <xref:System.Math> ou <xref:System.Convert>, você deve fornecer uma referência de assembly ao relatório para que o processador de relatórios possa resolver os nomes. Para obter mais informações, consulte [Adicionar código a um relatório &#40;SSRS&#41;](add-code-to-a-report-ssrs.md).  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>Para adicionar uma referência de assembly a um relatório  
  
1.  No modo de exibição de **Design** , clique com o botão direito do mouse na superfície de design fora da borda do relatório e clique em **Propriedades do Relatório**.  
  
2.  Clique em **Referências**.  
  
3.  Em **Adicionar ou remover assemblies**, clique em **Adicionar** e clique no botão de reticências para procurar para o assembly.  
  
4.  Em **Adicionar ou remover classes**, clique em **Adicionar** e digite o nome da classe e forneça um nome de instância a ser usado no relatório.  
  
    > [!NOTE]  
    >  Especifique uma classe e um nome de instância somente para membros com base em instâncias. Não especifique os membros estáticos na lista **Classes** . Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Usando assemblies personalizados com relatórios](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Caixa de diálogo Propriedades do Relatório, Referências](../report-properties-dialog-box-references.md)  
  
  
