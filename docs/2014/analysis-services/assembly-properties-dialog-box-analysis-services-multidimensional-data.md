---
title: Caixa de diálogo Propriedades do assembly (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.assemblyproperties.f1
ms.assetid: da1174d6-d82b-4337-ac19-7368dbd95a84
author: minewiskan
ms.author: owend
ms.openlocfilehash: fc203f0a4117a2f59e09a53308f0c26bbcbce85b
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527963"
---
# <a name="assembly-properties-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Propriedades do Assembly (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Propriedades do Assembly** no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para definir as propriedades de uma referência de assembly em um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . É possível exibir a caixa de diálogo **Propriedades do Assembly** clicando com o botão direito do mouse em um assembly no **Explorador de Objetos** e selecionando **Propriedades**.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome**|Digite para alterar o nome da referência de assembly.<br /><br /> Observação: a alteração deste valor não altera o nome do assembly referido pela referência de assembly, mas altera o nome usado pela instância ou banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ao fazer referência à referência de assembly.|  
|**ID**|Exibe o identificador do assembly referenciado para pela referência de assembly.|  
|**Descrição**|Digite para alterar a descrição da referência de assembly.|  
|**Criar Carimbo de Data/Hora**|Exibe a data e a hora de criação da referência de assembly.|  
|**Última Atualização de Esquema**|Exibe a data e a hora da última atualização dos metadados da referência de assembly.|  
|**Tipo**|Exibe o tipo da referência de assembly. Os seguintes valores são exibidos:<br /><br /> **Assembly .net**: a referência de assembly refere-se a um [!INCLUDE[msCoName](../includes/msconame-md.md)] assembly .NET Framework.<br /><br /> **Dll com**: a referência de assembly refere-se a uma biblioteca com.|  
|**Fonte**|Exibe a origem da referência de assembly. Essa propriedade normalmente contém o caminho completo e o nome de arquivo do assembly referido pela referência de assembly.|  
|**Conjunto de Permissões**|Selecione o conjunto de permissões usado para determinar acesso à referência de assembly. Para obter mais informações sobre os valores disponíveis para essa propriedade, consulte <xref:Microsoft.AnalysisServices.ClrAssembly.PermissionSet%2A> .|  
|**Informações sobre Representação**|Selecione a informações de representação a serem usadas ao acessar a referência de assembly. Para obter mais informações sobre os valores disponíveis para essa propriedade, consulte [Elemento ImpersonationInfo &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/impersonationinfo-element-assl)|  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Gerenciamento de assemblies de modelo multidimensional](multidimensional-models/multidimensional-model-assemblies-management.md)  
  
  
