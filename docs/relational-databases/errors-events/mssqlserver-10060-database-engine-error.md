---
title: MSSQLSERVER_10060 | Microsoft Docs
description: O cliente do SQL Server não pode se conectar ao servidor. Confira uma explicação do erro 10060 e possíveis soluções.
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "10060"
helpviewer_keywords:
- 10060 (Database Engine error)
ms.assetid: 28c21277-cad8-406c-a955-07933a56982a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: cb6a706a664adc8dbc86760b6d5e7b519b8a192a
ms.sourcegitcommit: 36fe62a3ccf34979bfde3e192cfa778505add465
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2020
ms.locfileid: "94521203"
---
# <a name="mssqlserver_10060"></a>MSSQLSERVER_10060
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|10060|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Ocorreu um erro ao estabelecer uma conexão com o servidor.  Ao conectar-se ao SQL Server, essa falha pode ser provocada porque, sob as configurações padrão, o SQL Server não permite conexões remotas. (provedor: Provedor TCP, erro: 0 – Falha em uma tentativa de conexão porque a parte conectada não respondeu corretamente após um período ou houve falha na conexão estabelecida devido a uma falha na resposta do host conectado.) (Microsoft SQL Server, Erro: 10060)|  
  
## <a name="explanation"></a>Explicação  
O cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode se conectar com o servidor. Esse erro pode ocorrer porque o firewall no servidor recusou a conexão ou o servidor não está configurado para aceitar conexões remotas.  
  
## <a name="user-action"></a>Ação do usuário  
Para resolver esse erro, tente uma das seguintes ações:  
  
-   Certifique-se de que você configurou o firewall no computador para permitir que essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceite conexões.  
  
-   Use a ferramenta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager para permitir que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceite conexões remotas.  
  
## <a name="see-also"></a>Consulte Também  
[Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](~/database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Protocolos de rede e bibliotecas de rede](~/sql-server/install/network-protocols-and-network-libraries.md)  
[Configuração de rede de cliente](~/database-engine/configure-windows/client-network-configuration.md)  
[Configurar protocolos de cliente](~/database-engine/configure-windows/configure-client-protocols.md)  
[Habilitar ou desabilitar um protocolo de rede do servidor](~/database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)  
  
