---
title: MSSQLSERVER_33129 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 33129 (Database Engine error)
ms.assetid: 83b5f368-f1a1-4a40-9bb6-c77e2dec690f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b49a78abd451249d293b350409e139f84966ed97
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85033660"
---
# <a name="mssqlserver_33129"></a>MSSQLSERVER_33129
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|33129|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_CANNOT_DISABLE_WIN_GROUP|  
|Texto da mensagem|Não é possível usar ALTER_LOGIN com o argumento DISABLE para negar acesso a um grupo do Windows.|  
  
## <a name="explanation"></a>Explicação  
 Esta mensagem ocorre na tentativa de desabilitar o logon de um Grupo do Windows.  
  
## <a name="user-action"></a>Ação do usuário  
 O logon de um Grupo do Windows não pode ser desabilitado. Para remover temporariamente a permissão de acesso concedida a um Grupo do Windows, revogue (REVOKE) a permissão CONNECT do logon para o Grupo do Windows. Os usuários do Windows possivelmente ainda deverão ter acesso por meio do logon individual ou através de outro Grupo do Windows. O exemplo a seguir revoga a permissão connect no Grupo de Contabilidade do domínio WESTCOAST.  
  
```sql  
REVOKE CONNECT TO [WESTCOAST\Accounting];  
```  
  
  
