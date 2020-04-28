---
title: Habilitando uma DLL para ser executada no DCOM | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DLL on DCOM in RDS [ADO]
- DCOM in RDS [ADO]
- business objects in RDS [ADO]
ms.assetid: 5f1c2205-191c-4fb4-9bd9-84c878ea46ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9ea7ea83219780602f8d8d68e5c807178e775bc2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67922709"
---
# <a name="enabling-a-dll-to-run-on-dcom"></a>Habilitar um DLL para ser executado no DCOM
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 As etapas a seguir descrevem como habilitar um objeto de negócios. dll para usar o DCOM e o Microsoft Serviços de Informações da Internet (HTTP) por meio de serviços de componentes.  
  
1.  Crie um novo pacote vazio no snap-in MMC dos serviços de componentes.  
  
     Você usará o snap-in MMC dos serviços de componentes para criar um pacote e adicionar a DLL a esse pacote. Isso torna o. dll acessível por meio do DCOM, mas remove a acessibilidade por meio do IIS. (Se você fizer check-in do registro para o. dll, a chave **InProc** estará vazia; definir o atributo de ativação, explicado mais adiante neste tópico, adicionará um valor na chave **InProc** .)  
  
2.  Instale um objeto comercial no pacote.  
  
     -ou-  
  
     Importe o objeto [RDSServer. datafactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) para o pacote.  
  
3.  Defina o atributo de ativação para o pacote como **no processo do criador** (aplicativo de biblioteca).  
  
     Para tornar o. dll acessível por meio do DCOM e do IIS no mesmo computador, você deve definir o atributo de ativação do componente no snap-in do MMC dos serviços de componentes. Depois de definir o atributo como **no processo do criador**, você observará que uma chave de servidor **InProc** no registro foi adicionada que aponta para um componente dos serviços de componentes substituto. dll.  
  
 Para obter mais informações sobre os serviços de componentes (ou o Microsoft Transaction Service, se você estiver usando o Windows NT) e como executar essas etapas, visite o site do Microsoft Transaction Server.


