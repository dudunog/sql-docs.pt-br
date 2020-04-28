---
title: Usar o driver ODBC do VFP FoxPro com seu aplicativo Visual Basic | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], visual basic applications
- Visual Basic applications [ODBC]
- FoxPro ODBC driver [ODBC], visual basic applications
- Visual FoxPro data [ODBC], visual basic applications
ms.assetid: 5223ca23-5df6-4ebc-aa3b-70682ff27a8c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 871c392166fa2f5726e6f9e8651bf758dc144a00
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292696"
---
# <a name="using-the-vfp-foxpro-odbc-driver-with-your-visual-basic-application"></a>Usar o Driver ODBC do VFP FoxPro com seu aplicativo Visual Basic
O aplicativo Microsoft® Visual Basic® pode se comunicar com os dados do Visual FoxPro criando um controle de dados que se conecta a uma fonte de dados do Visual FoxPro.  
  
#### <a name="to-connect-to-visual-foxpro-data-using-the-data-control-in-visual-basic"></a>Para se conectar aos dados do Visual FoxPro usando o controle de dados no Visual Basic  
  
1.  Crie uma fonte de dados chamada "Test" que se conecta ao banco de TasTrade de exemplo incluído no Visual FoxPro. A instalação padrão do Visual FoxPro coloca o banco de dados de exemplo TasTrade no local:  
  
    ```  
    c:\vfp\samples\mainsamp\data\tastrade.dbc  
    ```  
  
2.  No Visual Basic, crie um novo formulário e coloque uma caixa de texto e um controle de dados nele.  
  
3.  Altere a propriedade Connect do controle de dados da seguinte maneira:  
  
    ```  
    ODBC;DATABASE=tastrade;DSN=test  
    ```  
  
4.  Altere a propriedade RecordsetType para o seguinte:  
  
    ```  
    2 - Snapshot  
    ```  
  
5.  Altere a propriedade RecordName para o seguinte:  
  
    ```  
    customer  
    ```  
  
6.  Altere a propriedade DataSource da caixa de texto para o nome padrão do controle de dados para o seguinte:  
  
    ```  
    data1  
    ```  
  
7.  Altere a propriedade DataField da caixa de texto para o seguinte:  
  
    ```  
    customer_id  
    ```  
  
8.  Execute o formulário e use o controle de dados para ignorar os campos de ID do cliente do banco de dados de exemplo TasTrade do Visual FoxPro.
