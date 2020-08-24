---
description: Propriedade Item (conjunto de células do ADO MD)
title: Propriedade Item (ADO MD células) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Item
- Cellset::Item
helpviewer_keywords:
- Item property [ADO MD]
ms.assetid: 0e93d79b-b12e-4e98-889e-c2dfcca20fd0
author: rothja
ms.author: jroth
ms.openlocfilehash: 12df2a7d592be4fa42d8cc0df779a375ab987cb2
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778065"
---
# <a name="item-property-ado-md-cellset"></a>Propriedade Item (conjunto de células do ADO MD)
Recupera uma célula de um [células](./cellset-object-ado-md.md) usando suas coordenadas.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Set  
Cell = Cellset.Item ( Positions)  
```  
  
## <a name="parameters"></a>Parâmetros  
 *Posições*  
 Um **VariantArray** de valores que especificam exclusivamente uma célula. As *posições* podem ser uma das seguintes:  
  
-   Uma matriz de números de posição  
  
-   Uma matriz de nomes de membro  
  
-   A posição ordinal  
  
## <a name="remarks"></a>Comentários  
 Use a propriedade **Item** para retornar um objeto de [célula](./cell-object-ado-md.md) dentro de um objeto [células](./cellset-object-ado-md.md) . Se a propriedade **Item** não puder localizar a célula correspondente ao argumento *Positions* , ocorrerá um erro.  
  
 A propriedade **Item** é a propriedade padrão para o objeto **células** . As seguintes formas de sintaxe são intercambiáveis:  
  
```  
  
Cellset.Item ( Positions )Cellset ( Positions )  
```  
  
## <a name="remarks"></a>Comentários  
 O argumento *Positions* especifica qual célula retornar. Você pode especificar a célula pela posição ordinal ou pela posição ao longo de cada eixo. Ao especificar a célula por posição ao longo de cada eixo, você pode especificar o valor numérico da posição ou os nomes dos membros de cada posição.  
  
 A posição ordinal é um número que identifica exclusivamente uma célula dentro do **células**. Conceitualmente, as células são numeradas em um **células** como se o **células** fosse uma matriz *p*-dimensional, em que *p* é o número de eixos. As células são tratadas em ordem linha-principal. Abaixo está a fórmula para calcular o número ordinal de uma célula:  
  
 Se os nomes dos membros forem passados como cadeias de caracteres para o **Item**, os membros deverão ser listados em ordem crescente dos identificadores do eixo numérico. Dentro de um eixo, os membros devem ser listados em ordem crescente de aninhamento de dimensão – ou seja, o membro da dimensão mais externa vem primeiro, seguido por membros de dimensões internas. Cada dimensão deve ser representada por uma cadeia de caracteres separada, e a lista de cadeias de caracteres de membro deve ser separada por vírgulas.  
  
> [!NOTE]
>  A recuperação de células por nome de membro pode não ser suportada pelo seu provedor de dados. Consulte a documentação do seu provedor para obter mais informações.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto Cellset (ADO MD)](./cellset-object-ado-md.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Cell (ADO MD)](./cell-object-ado-md.md)   
 [Objeto Cellset (ADO MD)](./cellset-object-ado-md.md)