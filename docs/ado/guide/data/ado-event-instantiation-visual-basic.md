---
title: 'Instanciação de evento ADO: Visual Basic | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
ms.assetid: dce0a2a3-326f-4aaf-a822-6c5549833afa
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ead713a37d4ecf8bdfecd0d6c485684d1ad0777f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926074"
---
# <a name="ado-event-instantiation-visual-basic"></a>Instanciação de evento ADO: Visual Basic
Para manipular eventos ADO no Microsoft® Visual Basic®, você deve declarar uma variável em nível de módulo usando a palavra-chave **WithEvents** . A variável só pode ser declarada como parte de um módulo de classe e deve ser declarada no nível do módulo. No entanto, isso não é tão restritivo, porque Visual Basic objetos de **formulário** também são classes. A maneira mais simples de manipular eventos ADO é declarar uma variável usando **WithEvents**. O exemplo a seguir manipula o evento **ConnectComplete** para um objeto de **conexão** :  
  
```  
' BeginEventExampleVB02  
Dim WithEvents connEvent As Connection  
Attribute connEvent.VB_VarHelpID = -1  
  
Private Sub Form_Load()  
Dim strConn As String  
  
   ' Create a new object with event  
   ' handling enabled.  
   strConn = "Provider=sqloledb;" & _  
      "Data Source=MyServer;" & _  
      "Initial Catalog=Northwind;" & _  
      "Integrated Security=SSPI;"  
   Set connEvent = New ADODB.Connection  
   connEvent.Open strConn  
End Sub  
  
Private Sub connEvent_ConnectComplete(ByVal pError As ADODB.Error, _  
    adStatus As ADODB.EventStatusEnum, _  
    ByVal pConnection As ADODB.Connection)  
Dim strMsg As String  
  
   If adStatus = adStatusErrorsOccurred Then  
      Select Case pError.Number  
         Case adErrOperationCancelled  
            ' The operation was cancelled in the  
            ' Will event. Notify the user and exit.  
            strMsg = "I'm sorry you can't connect right now." & vbCrLf  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
         Case Else  
            strMsg = "Error " & Format(pError.Number) & vbCrLf  
            strMsg = strMsg & pError.Description  
            strMsg = strMsg & "Click OK to exit."  
            Unload Me  
      End Select  
   End If  
   frmWait.btnOK.Enabled = True  
End Sub  
' EndEventExampleVB02  
```  
  
 O objeto de **conexão** é declarado no nível de **formulário** usando a palavra-chave **WithEvents** para habilitar a manipulação de eventos. O manipulador de eventos de Form_Load, na verdade, cria o objeto atribuindo um novo objeto de **conexão** a *connEvent* e, em seguida, abre a conexão. É claro que um aplicativo real faria mais processamento no manipulador de eventos Form_Load do que é mostrado aqui.
