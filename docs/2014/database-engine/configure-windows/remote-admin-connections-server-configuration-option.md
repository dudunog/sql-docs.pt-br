---
title: Opção de configuração de servidor remote admin connections | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- administrator connections [SQL Server]
- DAC
- connections [SQL Server], dedicated administrator
- remote admin connections option
- dedicated administrator connections [SQL Server]
ms.assetid: bf32b60a-7a48-401f-b6be-b5e2e46c413f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 83d4b4e63e3f761b03db9024ca27a4da7f48a6b6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935106"
---
# <a name="remote-admin-connections-server-configuration-option"></a>Opção de configuração de servidor remote admin connections
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma DAC (conexão de administrador dedicada). A DAC permite que um administrador acesse um servidor em execução para desempenhar funções de diagnóstico ou executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , ou para solucionar problemas no servidor, mesmo quando o servidor está bloqueado ou está sendo executado em um estado anormal e não está respondendo a uma conexão com o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Por padrão, a DAC só está disponível a partir de um cliente no servidor. Para permitir que os aplicativos cliente de computadores remotos utilizem a DAC, use a opção remote admin connections sp_configure.  
  
 Por padrão, a DAC escuta apenas no endereço IP de loopback (127.0.0.1), porta 1434. Se a porta TCP 1434 não estiver disponível, uma porta TCP será atribuída dinamicamente quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for iniciado. Quando houver mais de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada em um computador, verifique o número da porta TCP no log de erros.  
  
 A tabela a seguir lista os possíveis valores para a opção remote admin connections.  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|0|Indica que apenas conexões locais são permitidas usando a DAC.|  
|1|Indica que são permitidas conexões remotas usando a DAC.|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir habilita a DAC a partir de um computador remoto.  
  
```  
sp_configure 'remote admin connections', 1;  
GO  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Conexão de diagnóstico para administradores de banco de dados](diagnostic-connection-for-database-administrators.md)  
  
  
