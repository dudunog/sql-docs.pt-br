---
title: Adicionar uma referência de assembly a um relatório | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
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
ms.openlocfilehash: c9725d51c934172c6c6291b6a7f1592a3ddc057c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080685"
---
# <a name="add-an-assembly-reference-to-a-report-ssrs"></a>Adicionar uma referência de assembly a um relatório (SSRS)
  Quando você insere o código personalizado que contém referências a classes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] que não estão no <xref:System.Math> ou <xref:System.Convert>, você deve fornecer uma referência de assembly ao relatório para que o processador de relatórios possa resolver os nomes. Para obter mais informações, consulte [Adicionar código a um relatório &#40;SSRS&#41;](../../reporting-services/report-design/add-code-to-a-report-ssrs.md).  
  
### <a name="to-add-an-assembly-reference-to-a-report"></a>Para adicionar uma referência de assembly a um relatório  
  
1.  No modo de exibição de **Design** , clique com o botão direito do mouse na superfície de design fora da borda do relatório e clique em **Propriedades do Relatório**.  
  
2.  Clique em **Referências**.  
  
3.  Em **Adicionar ou remover assemblies**, clique em **Adicionar** e clique no botão de reticências para procurar para o assembly.  
  
4.  Em **Adicionar ou remover classes**, clique em **Adicionar** e digite o nome da classe e forneça um nome de instância a ser usado no relatório.  
  
    > [!NOTE]  
    >  Especifique uma classe e um nome de instância somente para membros com base em instâncias. Não especifique os membros estáticos na lista **Classes** . Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Usando assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Caixa de diálogo Propriedades do Relatório, Referências](https://msdn.microsoft.com/library/4639d368-9918-4bb1-9953-7a724ca78dea)  
  
  
