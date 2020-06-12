---
title: Objetos ASSL e características de objeto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- reference exceptions [Analysis Services Scripting Language]
- ASSL, objects
- inheritance [Analysis Services Scripting Language]
- localized names [Analysis Services Scripting Language]
- objects [Analysis Services Scripting Language]
- names [Analysis Services Scripting Language]
- Analysis Services Scripting Language, objects
- expansion [Analysis Services Scripting Language]
ms.assetid: 6e5c28b5-c0bc-4ccd-82e5-e174bbb71386
author: minewiskan
ms.author: owend
ms.openlocfilehash: 76d57bb421a7f486983476a6549a5121ce88ee9b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545688"
---
# <a name="assl-objects-and-object-characteristics"></a>Objetos e características de objeto ASSL
  Os objetos da ASSL (Analysis Services Scripting Language) seguem diretrizes específicas a respeito de grupos de objetos, herança, nomenclatura, expansão e processamento.  
  
## <a name="object-groups"></a>Grupos de objetos  
 Todos os [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] objetos têm uma representação XML. Os objetos estão divididos em dois grupos:  
  
 **Objetos principais**  
 Os objetos principais podem ser criados, alterados e excluídos de forma independente. Entre eles, estão incluídos:  
  
-   Servidores  
  
-   Bancos de dados  
  
-   Dimensões  
  
-   Cubes  
  
-   Grupos de medidas  
  
-   Partições  
  
-   Perspectivas  
  
-   Modelos de mineração  
  
-   Funções  
  
-   Comandos associados a um servidor ou a um banco de dados  
  
-   Fontes de dados  
  
 Os objetos principais têm as seguintes propriedades para o rastreamento de seu histórico e de seu status.  
  
-   `CreatedTimestamp`  
  
-   `LastSchemaUpdate`  
  
-   `LastProcessed` (onde apropriado)  
  
> [!NOTE]  
>  A classificação de um objeto como um objeto principal afeta a forma como uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] tratará esse objeto e como ele será manipulado na linguagem de definição de objeto. No entanto, essa classificação não garante que as ferramentas de desenvolvimento e de gerenciamento do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] permitirão a criação, a modificação ou a exclusão independente desses objetos.  
  
 **Objetos secundários**  
 Os objetos secundários só podem ser criados, alterados ou excluídos como parte da criação, da alteração ou da exclusão do objeto principal pai. Entre eles, estão incluídos:  
  
-   Hierarquias e níveis  
  
-   Atributos  
  
-   Medidas  
  
-   Colunas do modelo de mineração  
  
-   Comandos associados a um cubo  
  
-   Agregações  
  
## <a name="object-expansion"></a>Expansão de objetos  
 A restrição `ObjectExpansion` pode ser usada para controlar o grau de expansão do XML ASSL retornado pelo servidor. As opções dessa restrição estão relacionadas na tabela a seguir.  
  
|Valor de enumeração|Permitido para\<Alter>|Description|  
|-----------------------|---------------------------|-----------------|  
|*ReferenceOnly*|não|Retorna somente o nome, a ID e o carimbo de data/hora do objeto solicitado e de todos os objetos principais contidos de forma recursiva.|  
|*ObjectProperties*|sim|Expande o objeto solicitado e os objetos secundários contidos, mas não retorna objetos principais contidos.|  
|*Expandobject*|não|Igual a *ObjectProperties*, mas também retorna o nome, a ID e o carimbo de data/hora para os principais objetos contidos.|  
|*ExpandFull*|sim|Expande completamente o objeto solicitado e todos os objetos recursivamente.|  
  
 Esta seção de referência de ASSL descreve a representação *ExpandFull* . Todos os outros níveis de `ObjectExpansion` derivam desse nível.  
  
## <a name="object-processing"></a>Processamento de objetos  
 A ASSL inclui elementos ou propriedades somente leitura (por exemplo, `LastProcessed`) que podem ser lidos na instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], mas que são omitidos quando os scripts de comando são enviados à instância. O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ignora valores modificados para elementos somente leitura sem aviso ou erro.  
  
 O [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] também ignora propriedades impróprias ou irrelevantes sem gerar erros de validação. Por exemplo, o elemento X só deve estar presente quando o elemento Y tiver um valor específico. A instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] ignora o elemento X em vez de validar aquele elemento em relação ao valor do elemento Y.  
  
  
