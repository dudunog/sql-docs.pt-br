---
description: MSSQLSERVER_18482
title: MSSQLSERVER_18482
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18482 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 42e8bf7a80659467c489d86b8a3ca944ceebe360
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797783"
---
# <a name="mssqlserver_18482"></a>MSSQLSERVER_18482
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|18482|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|REMLOGIN_INVALID_SITE|
|Texto da mensagem|Não foi possível estabelecer conexão com o servidor '%.ls', pois '%. ls' não está definido como servidor remoto. Verifique se especificou o nome de servidor correto. %.*ls|
||

## <a name="explanation"></a>Explicação

Esse erro ocorre quando você tenta executar uma RPC (chamada de procedimento remoto) de um servidor para outro (por exemplo, executando um procedimento armazenado em um computador remoto com uma instrução como `EXEC SERV_REMOTE.pubs..byroyalty`). Uma mensagem de erro semelhante à mostrada a seguir é relatada ao usuário

> Erro 18482: Não foi possível estabelecer conexão com o servidor \<SERV_REMOTE>, pois \<SERV_REMOTE> não está definido como um servidor remoto. Verifique se especificou o nome de servidor correto.

## <a name="cause"></a>Causa

Esse erro ocorre quando o SQL Server não pode executar uma chamada de procedimento remoto. Isso pode ser causado pela configuração incorreta de um servidor local. Para fazer uma chamada de procedimento remoto, primeiro, o SQL Server determina quem o servidor local está procurando com o nome do servidor com srvid = 0 em sysservers. Se uma entrada com srvid = 0 não for encontrada em sysservers ou se o nome do servidor com srvid = 0 pertencer a um nome de servidor diferente do nome do computador local do Windows, você receberá o erro.

## <a name="user-action"></a>Ação do usuário

Para determinar se o servidor local está configurado corretamente, examine a coluna `srvstatus` em master..sysservers. Esse valor deve ser 0 para o servidor local.

Por exemplo, suponha que o servidor local tenha sido nomeado como SERV_LOCAL, o servidor remoto, *SERV_REMOTE*, e sysservers continha as seguintes informações:

|srvid|srvstatus|srvname|srvname|
|---|---|---|---|
|1|2|SERV_LOCAL|SERV_LOCAL|
|2|1|SERV_REMOTE|SERV_REMOTE|
||||

Na saída anterior, SERV_LOCAL é o servidor local, mas ele tem um srvid igual a 1, que deverá ser 0. Para corrigir isso, siga estas etapas:

1. Execute `sp_dropserver` local_server_name, droplogins (neste exemplo, você executará `sp_dropserver SERV_LOCAL, droplogins`).
1. Execute `sp_addserver` local_server_name, LOCAL (neste exemplo, você executará `sp_addserver SERV_LOCAL, LOCAL`).
1. Pare e reinicie o SQL Server.

Depois que você executar essas etapas, a tabela sysservers será semelhante à seguinte:

|srvid|srvstatus|srvname|srvname|
|---|---|---|---|
|0|0|SERV_LOCAL|SERV_LOCAL|
|2|1|SERV_REMOTE|SERV_REMOTE|
||||

> [!NOTE]
> A ID do Servidor (srvid) deverá ser 0 para o servidor local.

Pode haver alguns casos em que as entradas da tabela sysservers pareçam corretas, mas quando você executa `select @@servername`, ela retorna NULL. Nesses cenários, você ainda deverá executar as Etapas 1 a 3 listadas acima para corrigir o problema.

## <a name="more-information"></a>Mais informações

Você poderá receber esta mensagem de erro ao instalar a replicação, porque o processo de instalação faz chamadas de procedimento remoto entre os servidores envolvidos na replicação.
