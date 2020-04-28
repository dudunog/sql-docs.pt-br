---
title: Programando procedimentos armazenados estendidos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- gateway applications [SQL Server]
- extended stored procedures [SQL Server], about extended stored procedures
- Open Data Services [SQL Server]
- ODS [SQL Server]
ms.assetid: 561305cd-c803-48af-9eec-2c19f4d311ce
author: rothja
ms.author: jroth
ms.openlocfilehash: 541f24693598d20925dd37d4970c6d9916945793
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68032013"
---
# <a name="database-engine-extended-stored-procedures---programming"></a>Procedimento armazenado estendido do mecanismo do banco de dados – Programação +
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 No passado, o Open Data Services era usado para gravar aplicativos de servidor, como gateways para ambientes de banco de dados que não fossem o SQL Server. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o não oferece suporte a partes obsoletas da API Open Data Services. A única parte da API Open Data Services original ainda suportada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é a das funções de procedimento armazenado estendido, de modo que a API foi renomeada para a API de procedimento armazenado estendido.  
  
 Com o surgimento de tecnologias mais novas e mais avançadas, como as consultas distribuídas e a integração CLR, a necessidade por aplicativos de API de procedimento armazenado estendido foi amplamente substituída.  
  
> [!NOTE]  
>  Se você tiver aplicativos de gateway existentes, não poderá usar opends60.dll que acompanha o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar os aplicativos. Os aplicativos de gateway já não são mais suportados.  
  
## <a name="extended-stored-procedures-vs-clr-integration"></a>Procedimentos armazenados estendidos e Integração de CLR  
 Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os procedimentos armazenados estendidos forneciam o único mecanismo disponível para os desenvolvedores de aplicativos de banco de dados gravarem lógica no lado do servidor, o que era difícil de expressar ou impossível de gravar no [!INCLUDE[tsql](../../includes/tsql-md.md)]. A Integração CLR fornece uma alternativa mais robusta para gravar esses procedimentos. Além disso, com a Integração CLR, a lógica que costumava ser gravada na forma de procedimentos armazenados é, em geral, melhor expressada como funções com valor de tabela, o que permite que os resultados criados pela função sejam consultados nas instruções SELECT, inserindo-os na cláusula FROM.  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral da integração do CLR&#41; &#40;Common Language Runtime](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md)   
 [Funções com valor de tabela CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
  
  
