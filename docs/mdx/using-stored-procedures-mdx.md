---
description: Usando procedimentos armazenados (MDX)
title: Usando procedimentos armazenados (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 095a4ab1b3acd4ec5a238f19c27446b7cebe27b2
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196925"
---
# <a name="using-stored-procedures-mdx"></a>Usando procedimentos armazenados (MDX)


  Você pode estender a funcionalidade do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e da linguagem MDX gravando procedimentos armazenados .NET ou funções definidas pelo usuário. Para obter mais informações, consulte [programação de servidor ADOMD.net](/analysis-services/adomd/multidimensional-models-adomd-net-server/adomd-net-server-programming)  
  
 Quando você faz referência ou chama um procedimento armazenado, você especifica o nome da função seguido por parênteses. Dentro dos parênteses, você pode especificar expressões chamadas argumentos que fornecem dados a serem transmitidos nos parâmetros. Quando você chama uma função, deve fornecer valores de argumentos para todos os parâmetros e especificar os valores de argumentos na mesma sequência na qual os parâmetros são definidos na função definida pelo usuário.  
  
 A consulta de exemplo a seguir supõe que você tem um assembly nomeado SampleAssembly registrado no seu [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Server:  
  
```  
SELECT SampleAssembly.RandomSample([Geography].[State-Province].Members, 5) on ROWS,   
[Date].[Calendar].[Calendar Year] on COLUMNS  
FROM [Adventure Works]  
WHERE [Measures].[Reseller Freight Cost]  
```  
  
> [!NOTE]  
>  O *procedimento armazenado* é a terminologia usada no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para esses tipos de funções. Versões anteriores do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] chamaram esses tipos de funções como *funções definidas pelo usuário*.  
  
## <a name="types-of-stored-procedures"></a>Tipos de procedimentos armazenados  
 O [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] oferece suporte a assemblies COM e CLR. Recomenda-se assemblies CLR por causa da segurança reforçada disponível para assemblies CLR. Se o Microsoft Office Excel estiver instalado no servidor, as funções do Excel também estarão disponíveis.  
  
> [!NOTE]  
>  Os assemblies COM do Microsoft Visual Basic for Applications (VBA) são automaticamente registrados.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções &#40;sintaxe MDX&#41;](../mdx/functions-mdx-syntax.md)  
  
