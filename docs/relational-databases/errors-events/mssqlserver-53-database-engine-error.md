---
title: MSSQLSERVER_53 | Microsoft Docs
description: O cliente do SQL Server não pode se conectar ao servidor. Confira uma explicação do erro 53 e possíveis soluções.
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "53"
helpviewer_keywords:
- 53 (Database Engine error)
ms.assetid: 1234f5a2-b3d1-425a-b29f-480fa792305f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: e38abeb865418637336b88f8e1a72380c826a8e8
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521061"
---
# <a name="mssqlserver_53"></a>MSSQLSERVER_53
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|53|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Ocorreu um erro ao estabelecer uma conexão com o servidor.  Ao conectar-se ao SQL Server, essa falha pode ser provocada porque, sob as configurações padrão, o SQL Server não permite conexões remotas. (provedor: Provedor de Pipes Nomeados, erro: 40 – não foi possível abrir uma conexão com o SQL Server) (Provedor de Dados SqlClient do .Net)|  
  
## <a name="explanation"></a>Explicação  
O cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar com o servidor. Esse erro pode ocorrer porque o cliente não pode resolver o nome do servidor ou porque o nome do servidor está incorreto.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se você digitou o nome correto do servidor no cliente e se é possível resolver o nome do servidor no cliente. Para verificar a resolução de nomes TCP/IP, é possível usar o comando **ping** no sistema operacional Windows.  
  
## <a name="see-also"></a>Consulte Também  
[Protocolos de rede e bibliotecas de rede](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Configuração de rede de cliente](~/database-engine/configure-windows/client-network-configuration.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Habilitar ou desabilitar um protocolo de rede do servidor](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
