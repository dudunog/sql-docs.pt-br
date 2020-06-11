---
title: Adicionar colunas a uma estrutura de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], columns
- columns [data mining], mining structure columns
- adding columns
ms.assetid: 3f879344-9f66-4178-851a-e8c5ccccf4cb
author: minewiskan
ms.author: owend
ms.openlocfilehash: 13a8343fe83b29499c9fc52f40a7800884cd86cf
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84525612"
---
# <a name="add-columns-to-a-mining-structure"></a>Adicionar colunas a uma estrutura de mineração
  Use o Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para adicionar colunas a uma estrutura de mineração depois de defini-la no Assistente de Mineração de Dados. É possível adicionar qualquer coluna existente na exibição de fonte de dados que foi usada para definir a estrutura de mineração.  
  
> [!NOTE]  
>  Você pode adicionar várias cópias de colunas em uma estrutura de mineração, porém deve evitar o uso de mais de uma instância da coluna dentro do mesmo modelo, a fim de impedir correlações falsas entre a coluna de origem e a coluna derivada.  
  
### <a name="to-add-a-column-to-a-mining-structure"></a>Para adicionar uma coluna a uma estrutura de mineração  
  
1.  Selecione a guia **Estrutura de Mineração** no Designer de Mineração de Dados.  
  
2.  Clique com o botão direito do mouse na estrutura de mineração e selecione **Adicionar uma Coluna**.  
  
     A caixa de diálogo **Selecionar uma Coluna** é exibida.  
  
3.  Em **Tabela de Origem**, selecione a tabela na exibição de fonte de dados em que reside a coluna.  
  
4.  Em **Coluna de origem**, selecione a coluna que você quer adicionar à estrutura de mineração.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  Se você adicionar uma coluna existente, uma cópia será incluída na estrutura, e o nome anexado com um "1". Você pode alterar o nome da coluna copiada para algo mais descritivo digitando um novo nome na propriedade **Nome** da coluna da estrutura de mineração.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções da estrutura de mineração](mining-structure-tasks-and-how-tos.md)  
  
  
