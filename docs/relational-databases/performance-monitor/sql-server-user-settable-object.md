---
title: SQL Server, objeto Definível pelo usuário | Microsoft Docs
description: Saiba mais sobre o objeto User Settable, que cria instâncias de contador personalizadas no SQL Server para monitorar aspectos do servidor que não são monitorados pelos contadores existentes.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- User Settable object
- SQLServer:User Settable
ms.assetid: 633de3ef-533c-4f0c-9c7b-c105129d8e94
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 980a7161eba7cc40da6de3f2c4172df7e2349c78
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505554"
---
# <a name="sql-server-user-settable-object"></a>SQL Server, objeto User Settable
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O objeto **User Settable** no Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite criar instâncias de contador personalizadas. Use instâncias de contador personalizadas para monitorar aspectos do servidor que escapam aos contadores existentes, como componentes exclusivos de seu banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (por exemplo, o número de pedidos de clientes registrados em log ou o estoque de produtos).  
  
 O objeto **Definível pelo Usuário** contém 10 instâncias do contador de consulta: **Contador de usuário 1** a **Contador do usuário 10**. Esses contadores são mapeados para os procedimentos armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de **sp_user_counter1** a **sp_user_counter10**. À medida que esses procedimentos armazenados são executados por aplicativos do usuário, os valores definidos por eles são exibidos no Monitor do Sistema. Um contador pode monitorar qualquer valor inteiro individual (por exemplo, um procedimento armazenado que conta quantos pedidos de um produto em particular ocorreram em um dia).  
  
> [!NOTE]  
>  Os procedimentos armazenados de contadores do usuário não são sondados automaticamente pelo Monitor do Sistema. Eles devem ser executados explicitamente por um aplicativo de usuário para obter os valores de contador a serem atualizados. Use um gatilho para atualizar o valor do contador automaticamente. Por exemplo, para criar um contador que monitore o número de linhas em uma tabela, crie um gatilho INSERT e DELETE na tabela que executa a seguinte instrução: `SELECT COUNT(*) FROM table`. Sempre que o gatilho for acionado devido à ocorrência de operação INSERT ou DELETE na tabela, o contador do Monitor do Sistema será atualizado automaticamente.  
  
 Essa tabela descreve o objeto **User Settable** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores do SQL Server definíveis pelo usuário|Descrição|  
|---------------------------------------|-----------------|  
|**Consulta**|O objeto **User Settable** contém o contador da consulta. Os usuários configuram os **Contadores do usuário** dentro do objeto de consulta.|  
  
 Essa tabela descreve as **instâncias** do contador de **Consultas** .  
  
|Instâncias do contador de consultas|Descrição|  
|-----------------------------|-----------------|  
|**Contador do usuário 1**|Definido usando **sp_user_counter1**.|  
|**Contador do usuário 2**|Definido usando **sp_user_counter2**.|  
|**Contador do usuário 3**|Definido usando **sp_user_counter3**.|  
|...||  
|**Contador do usuário 10**|Definido usando **sp_user_counter10**.|  
  
 Para usar os procedimentos armazenados de contador do usuário, execute-os a partir de seu próprio aplicativo com um único parâmetro de inteiro representando o novo valor do contador. Por exemplo, para definir o **Contador do usuário 1** com o valor 10, execute essa instrução Transact-SQL:  
  
```  
EXECUTE sp_user_counter1 10  
```  
  
 Os procedimentos armazenados de contador do usuário podem ser chamados a partir de qualquer lugar onde normalmente podem ser chamados os outros procedimentos armazenados, como os seus próprios procedimentos armazenados. Por exemplo, é possível criar o seguinte procedimento armazenado para contar o número de conexões e tentativas de conexão desde que foi iniciada a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
```  
DROP PROC My_Proc  
GO  
CREATE PROC My_Proc  
AS   
   EXECUTE sp_user_counter1 @@CONNECTIONS  
GO  
```  
  
 A função @[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retorna o número de conexões ou tentativas de conexão desde o início de uma instância de @CONNECTIONS. Esse valor é passado ao procedimento armazenado **sp_user_counter1** como parâmetro.  
  
> [!IMPORTANT]  
>  Torne as consultas definidas nos procedimentos armazenados de contador do usuário o mais simples possível. Consultas que consomem muita memória e realizam operações substanciais de classificação ou hash ou grandes quantidades de E/S são de execução dispendiosa e podem influir no desempenho.  
  
## <a name="permissions"></a>Permissões  
 **sp_user_counter** está disponível para todos os usuários, mas pode ser restringido para qualquer contador de consultas.  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
