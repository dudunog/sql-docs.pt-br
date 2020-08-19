---
description: Conceitos básicos do ADO MD
title: Conceitos básicos de ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, fundamentals
ms.assetid: f6a20d9f-c1ab-474c-b9f3-82277e2a126d
author: rothja
ms.author: jroth
ms.openlocfilehash: fec7d924003df2a0c0c20b5ca2b0de9162cfd1c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452438"
---
# <a name="ado-md-fundamentals"></a>Conceitos básicos do ADO MD
O Microsoft® ActiveX® Data Objects (Multidimensional) (ADO MD) fornece acesso fácil a dados multidimensionais de linguagens como Microsoft Visual Basic®, Microsoft Visual C++®. ADO MD estende o Microsoft ActiveX® Data Objects (ADO) para incluir objetos específicos de dados multidimensionais, como os objetos [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) e [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) . Com ADO MD você pode procurar o esquema multidimensional, consultar um cubo e recuperar os resultados.  
  
 Assim como o ADO, o ADO MD usa um provedor de OLE DB subjacente para obter acesso aos dados. Para trabalhar com ADO MD, o provedor deve ser um MDP (provedor de dados multidimensional), conforme definido pelo OLE DB para especificação de OLAP. Um MDP apresenta dados em exibições multidimensionais em vez de exibições tabulares, que é como um provedor de dados de tabela (TDP) apresenta dados. Consulte a documentação do seu provedor de OLE DB OLAP para obter mais informações sobre a sintaxe e o comportamento específicos com suporte no seu provedor.  
  
 Este documento pressupõe um conhecimento prático da linguagem de programação Visual Basic e um conhecimento geral do ADO e do OLAP. Para obter mais informações, consulte o [Guia do programador de ADO](../../../ado/guide/ado-programmer-s-guide.md) e [OLE DB para OLAP (processamento analítico online)](https://msdn.microsoft.com/library/windows/desktop/ms717005.aspx).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Visão geral de dados e esquemas multidimensionais](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)  
  
-   [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)  
  
-   [Usar o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)  
  
-   [Programar com o ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Guia do programador do ADO](../../../ado/guide/ado-programmer-s-guide.md)   
 [Extensões ADO para linguagem de definição de dados e segurança (ADOX)](../../../ado/guide/extensions/ado-extensions-for-data-definition-language-and-security-adox.md)   
 [Visão geral de esquemas multidimensionais e dados](../../../ado/guide/multidimensional/overview-of-multidimensional-schemas-and-data.md)   
 [Programando com ADO MD](../../../ado/guide/multidimensional/programming-with-ado-md.md)   
 [Usando o ADO com ADO MD](../../../ado/guide/multidimensional/using-ado-with-ado-md.md)   
 [Manipular dados multidimensionais](../../../ado/guide/multidimensional/working-with-multidimensional-data.md)
