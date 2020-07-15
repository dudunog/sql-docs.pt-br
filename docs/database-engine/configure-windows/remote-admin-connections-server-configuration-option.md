---
title: Opção de configuração de servidor remote admin connections | Microsoft Docs
description: Saiba como os aplicativos em computadores remotos podem usar o DAC. Confira como usar a opção "conexões de administrador remoto" com "sp_configure" para ativar essa funcionalidade.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9d7aa4d4b6658461be3a4fc5c762b3cef5343be4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85651730"
---
# <a name="remote-admin-connections-server-configuration-option"></a>Opção de configuração de servidor remote admin connections
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma DAC (conexão de administrador dedicada). A DAC permite que um administrador acesse um servidor em execução para desempenhar funções de diagnóstico ou executar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] , ou para solucionar problemas no servidor, mesmo quando o servidor está bloqueado ou está sendo executado em um estado anormal e não está respondendo a uma conexão com o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Por padrão, a DAC só está disponível a partir de um cliente no servidor. Para permitir que os aplicativos cliente de computadores remotos utilizem a DAC, use a opção remote admin connections sp_configure.  
  
 Por padrão, a DAC escuta apenas no endereço IP de loopback (127.0.0.1), porta 1434. Se a porta TCP 1434 não estiver disponível, uma porta TCP será atribuída dinamicamente quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] for iniciado. Quando houver mais de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada em um computador, verifique o número da porta TCP no log de erros.  
  
 A tabela a seguir lista os possíveis valores para a opção remote admin connections.  
  
|Valor|Descrição|  
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
 [Conexão de diagnóstico para administradores de banco de dados](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)  
  
  
