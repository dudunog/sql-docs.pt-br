---
description: Exemplo dos métodos CopyRecord, CopyTo e SaveToFile (VB)
title: Exemplo dos métodos CopyRecord, CopyTo e SaveToFile (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- CopyRecord method [ADO], Visual Basic example
- SaveToFile method [ADO], Visual Basic example
- CopyTo method [ADO], Visual Basic example
ms.assetid: 61a51b74-93cd-439c-877f-f3055499d39f
author: rothja
ms.author: jroth
ms.openlocfilehash: d19c7a994cd4db7d65a285e523726c0bdd88f582
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444388"
---
# <a name="copyrecord-copyto-and-savetofile-methods-example-vb"></a>Exemplo dos métodos CopyRecord, CopyTo e SaveToFile (VB)
Este exemplo demonstra como criar cópias de um arquivo usando objetos [Stream](../../../ado/reference/ado-api/stream-object-ado.md) ou [Record](../../../ado/reference/ado-api/record-object-ado.md) . Uma cópia é feita em uma pasta da Web para publicação na Internet. Outras propriedades e métodos mostrados incluem [tipo de fluxo](../../../ado/reference/ado-api/type-property-ado-stream.md), **abrir**, [LoadFromFile](../../../ado/reference/ado-api/loadfromfile-method-ado.md)e [registro aberto](../../../ado/reference/ado-api/open-method-ado-record.md).  
  
```  
'BeginCopyRecordVB  
  
'Note:  
' This sample requires that "C:\checkmrk.wmf" and  
' "https://MyServer/mywmf.wmf" exist.  
  
Option Explicit  
  
Private Sub Form_Load()  
    On Error GoTo ErrorHandler  
  
    ' Declare variables  
    Dim strPicturePath, strStreamPath, strStream2Path, _  
        strRecordPath, strStreamURL, strRecordURL As String  
    Dim objStream, objStream2 As Stream  
    Dim objRecord As Record  
    Dim objField As Field  
  
    ' Instantiate objects  
    Set objStream = New Stream  
    Set objStream2 = New Stream  
    Set objRecord = New Record  
  
    ' Initialize path and URL strings  
    strPicturePath = "C:\checkmrk.wmf"  
    strStreamPath = "C:\mywmf.wmf"  
    strStreamURL = "URL=https://MyServer/mywmf.wmf"  
    strStream2Path = "C:\checkmrk2.wmf"  
    strRecordPath = "C:\mywmf.wmf"  
    strRecordURL = "https://MyServer/mywmf2.wmf"  
  
    ' Load the file into the stream  
    objStream.Open  
    objStream.Type = adTypeBinary  
    objStream.LoadFromFile (strPicturePath)  
  
    ' Save the stream to a new path and filename  
    objStream.SaveToFile strStreamPath, adSaveCreateOverWrite  
  
    ' Copy the contents of the first stream to a second stream  
    objStream2.Open  
    objStream2.Type = adTypeBinary  
    objStream.CopyTo objStream2  
  
    ' Save the second stream to a different path  
    objStream2.SaveToFile strStream2Path, adSaveCreateOverWrite  
  
    ' Because strStreamPath is a Web Folder, open a Record on the URL  
    objRecord.Open "", strStreamURL  
  
    ' Display the Fields of the record  
    For Each objField In objRecord.Fields  
        Debug.Print objField.Name & ": " & objField.Value  
    Next  
  
    ' Copy the record to a new URL  
    objRecord.CopyRecord "", strRecordURL, , , adCopyOverWrite  
  
    ' Load each copy of the graphic into Image controls for viewing  
    Image1.Picture = LoadPicture(strPicturePath)  
    Image2.Picture = LoadPicture(strStreamPath)  
    Image3.Picture = LoadPicture(strStream2Path)  
    Image4.Picture = LoadPicture(strRecordPath)  
  
    ' clean up  
    objStream.Close  
    objStream2.Close  
    objRecord.Close  
    Set objStream = Nothing  
    Set objStream2 = Nothing  
    Set objRecord = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not objStream Is Nothing Then  
        If objStream.State = adStateOpen Then objStream.Close  
    End If  
    Set objStream = Nothing  
  
    If Not objStream2 Is Nothing Then  
        If objStream2.State = adStateOpen Then objStream2.Close  
    End If  
    Set objStream2 = Nothing  
  
    If Not objRecord Is Nothing Then  
        If objRecord.State = adStateOpen Then objRecord.Close  
    End If  
    Set objRecord = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndCopyRecordVB  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Método CopyRecord (ADO)](../../../ado/reference/ado-api/copyrecord-method-ado.md)   
 [Método CopyTo (ADO)](../../../ado/reference/ado-api/copyto-method-ado.md)   
 [Método LoadFromFile (ADO)](../../../ado/reference/ado-api/loadfromfile-method-ado.md)   
 [Método Open (registro ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)   
 [Método Open (fluxo ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)   
 [Objeto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)   
 [Propriedade Type (Fluxo ADO)](../../../ado/reference/ado-api/type-property-ado-stream.md)
