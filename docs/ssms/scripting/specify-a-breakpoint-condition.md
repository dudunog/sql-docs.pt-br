---
title: Especificar uma condição de ponto de interrupção
description: Saiba como estabelecer uma condição de ponto de interrupção para controlar se o depurador executa uma ação de ponto de interrupção quando o ponto de interrupção é atingido e a contagem de ocorrências é atingida.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoint conditions
ms.assetid: b43d8a2b-99a3-4fb7-8848-99c042ea7ef7
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.reviewer: ''
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c9e8343d1743d90472d10095e18e66294b9ea99b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97466247"
---
# <a name="specify-a-breakpoint-condition"></a>Especificar uma condição de ponto de interrupção

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Uma condição de ponto de interrupção é uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] que é avaliada pelo depurador ao atingir o ponto de interrupção. Se a condição for atendida e qualquer contagem de ocorrências especificada for atingida, o depurador será interrompido ou executará a ação especificada para o ponto de interrupção.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="specifying-conditions"></a>Especificando condições

A expressão especificada deve ser uma expressão Transact-SQL válida que seja avaliada como um valor Booliano. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
 Se você especificar uma condição de ponto de interrupção com sintaxe inválida, será exibida uma mensagem de aviso imediatamente. Se você especificar uma condição com sintaxe válida, mas semântica inválidas, será exibida uma mensagem de aviso da primeira vez que o ponto de interrupção for atingido. Em qualquer um dos casos, o depurador interromperá a execução quando o ponto de interrupção inválido for atingido.  
  
#### <a name="to-specify-a-condition"></a>Para especificar uma condição
  
1. Na janela do editor, clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Condição** no menu de atalho.  
  
     -ou-  
  
     Na janela **Pontos de Interrupção** , clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Condição** no menu de atalho.  
  
2. Na caixa de diálogo **Condição de Ponto de Interrupção** , insira uma expressão Booliana válida na caixa **Condição** .  
  
3. Escolha **Is true** para interromper quando a expressão for avaliada como **true** ou escolha **Has changed** para interromper quando o valor da expressão for alterado.  
  
    > [!NOTE]  
    >  O depurador não avalia a expressão Booliana até a primeira vez que o ponto de interrupção é atingido. Se você escolher **Has changed**, o depurador não considerará a primeira avaliação como uma alteração, então o depurador não interromperá na primeira avaliação.  
  
## <a name="see-also"></a>Consulte Também

- [Especificar uma contagem de ocorrências](./specify-a-hit-count.md)
- [Especificar uma ação de ponto de interrupção](./specify-a-breakpoint-action.md)