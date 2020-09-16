---
title: Especificar uma contagem de ocorrências
description: Saiba como definir uma contagem de ocorrências para um ponto de interrupção, de modo que o depurador não interrompa nesse ponto de interrupção até que a contagem de ocorrências seja alcançada.
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vs.debug.breakpt.hitcount
helpviewer_keywords:
- Transact-SQL debugger, breakpoint hit count
ms.assetid: 24836939-94ed-4e57-aa85-5d6938d859e4
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d83f361efd4d822456366133729759cb16c18647
ms.sourcegitcommit: 6d53ecfdc463914f045c20eda96da39dec22acca
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/26/2020
ms.locfileid: "88901418"
---
# <a name="specify-a-hit-count"></a>Especificar uma contagem de ocorrências

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Uma contagem de ocorrências de ponto de interrupção é um contador incrementado pelo depurador do [!INCLUDE[tsql](../../includes/tsql-md.md)] a cada vez que o ponto de interrupção é atingido. Se a contagem de ocorrências especificada for atingida, e qualquer condição de ponto de interrupção especificada for atendida, o depurador executará a ação especificada para o ponto de interrupção.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="hit-count-considerations"></a>Considerações sobre a contagem de ocorrências

 Por padrão, a execução é interrompida sempre que um ponto de interrupção é atingido. Você pode escolher uma das seguintes opções:  
  
-   Interromper sempre (o padrão).  
  
-   Interromper quando a contagem de ocorrências for igual a um valor especificado.  
  
-   Interromper quando a contagem de ocorrências for igual a um múltiplo do valor especificado.  
  
-   Interromper quando a contagem de ocorrências for maior ou igual ao valor especificado.  
  
 As contagens de ocorrências de ponto de interrupção são incrementadas dentro do escopo de uma sessão de depuração. Todas as contagens de ocorrências são definidas como zero no início de cada sessão de depuração.  
  
 Se você desejar controlar quantas vezes um ponto de interrupção é atingido sem ter a execução do ponto de interrupção, especifique uma contagem de ocorrências com um valor muito alto para que o ponto de interrupção nunca interrompa.  
  
 A ação padrão de um ponto de interrupção é interromper a execução quando a contagem de ocorrências e a condição de ponto de interrupção são atendidas. Para obter mais informações sobre como especificar outra ações, consulte [Especificar uma ação de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-action.md).  
  
#### <a name="to-specify-a-hit-count"></a>Para especificar uma contagem de ocorrências  
  
1.  Na janela do editor, clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Contagem de Ocorrências** no menu de atalho.  
  
     -ou-  
  
     Na janela **Pontos de Interrupção** , clique com o botão direito do mouse no glifo de ponto de interrupção e clique em **Contagem de Ocorrências** no menu de atalho.  
  
2.  Na caixa de diálogo **Contagem de Ocorrências de Ponto de interrupção** , selecione o comportamento desejado na caixa **Quando o ponto de interrupção for atingido** .  
  
     Se você escolher qualquer configuração diferente de **Interromper Sempre**, uma caixa de texto será exibida à direita da lista. Digite um inteiro na caixa de texto para especificar a contagem de ocorrências desejada.  
  
3.  Clique em **OK** para implementar as alterações ou em **Cancelar** para sair sem aplicar as alterações.  
  
#### <a name="to-view-or-reset-the-current-hit-count"></a>Para exibir ou redefinir a contagem de ocorrências atual  
  
1.  Na janela do editor, clique com o botão direito do mouse no glifo do ponto de interrupção e clique em **Contagem de Ocorrências** no menu de atalho.  
  
     -ou-  
  
     Na janela **Pontos de Interrupção** , clique com o botão direito do mouse no glifo de ponto de interrupção e clique em **Contagem de Ocorrências** no menu de atalho.  
  
2.  Na caixa de diálogo **Contagem de Ocorrências de Ponto de interrupção** , **Contagem de ocorrências atual:** é exibido imediatamente acima do botão **Redefinir** .  
  
3.  Clique em **Redefinir** se desejar definir a contagem de ocorrências atual como zero.  
  
4.  Clique em **OK** ou em **Cancelar** para sair do diálogo.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar uma condição de ponto de interrupção](../../relational-databases/scripting/specify-a-breakpoint-condition.md)  
  
  
