---
description: 'Etapa 4: Preencher a caixa de texto de detalhes'
title: 'Etapa 4: preencher a caixa de texto de detalhes | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: cb4273e2-c907-4a86-a621-3bf110088228
author: rothja
ms.author: jroth
ms.openlocfilehash: 868066b8225a3e87a2aad37ddd7569cc5be6bd75
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979477"
---
# <a name="step-4-populate-the-details-text-box"></a>Etapa 4: Preencher a caixa de texto de detalhes
Para preencher a caixa de texto detalhes, crie uma nova sub-rotina chamada **recFields** e insira o código a seguir:  
  
```  
Sub recFields(r As Record, l As ListBox, t As TextBox)  
    Dim f As Field  
    Dim s As Stream  
    Set s = New Stream  
    Dim str As String  
  
    For Each f In r.Fields  
        l.AddItem f.Name & ": " & f.Value  
    Next  
    t.Text = ""  
    If r!RESOURCE_CONTENTCLASS = "text/plain" Then  
        s.Open r, adModeRead, adOpenStreamFromRecord  
        str = s.ReadText(1)  
        s.Position = 0  
        If Asc(Mid(str, 1, 1)) = 63 Then '//63 = "?"  
            s.Charset = "ascii"  
            s.Type = adTypeText  
        End If  
        t.Text = s.ReadText(adReadAll)  
    End If  
End Sub  
```  
  
 Esse código é preenchido `lstDetails` com os campos e valores do registro simples passado para `recFields` . Se o recurso for um arquivo de texto, um fluxo de texto será aberto do registro de recurso. O código determina se o conjunto de caracteres é ASCII e copia o conteúdo do fluxo para `txtDetails` .  
  
## <a name="see-also"></a>Consulte Também  
 [Cenário de publicação na Internet](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Etapa 3: Preencher a caixa de listagem de campos](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
