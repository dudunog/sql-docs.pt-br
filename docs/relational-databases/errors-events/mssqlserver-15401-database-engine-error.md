---
description: MSSQLSERVER_15401
title: MSSQLSERVER_15401
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15401 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: c7a3153a34088b6b75c9b51f0cf8829049edfc6e
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797743"
---
# <a name="mssqlserver_15401"></a>MSSQLSERVER_15401
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|15401|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|SEC_INVALIDLOGINORGROUP|
|Texto da mensagem|Usuário ou grupo do Windows NT '%s' não encontrado. Verifique o nome novamente.|
||

## <a name="explanation"></a>Explicação

Esse erro ocorre quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode criar um logon com base na entidade de segurança do Windows (como um usuário de domínio ou um grupo de domínio do Windows). Uma mensagem de erro semelhante à mostrada a seguir é relatada ao usuário

> Erro 15401: Usuário ou grupo do Windows NT '%s' não encontrado. Verifique o nome novamente.

## <a name="cause"></a>Causa

O erro pode ocorrer devido a um dos seguintes motivos:

- O logon não existe no Active Directory.
- O controlador de domínio não está disponível.
- Você não está usando BUILTIN como o nome de domínio ao adicionar uma conta local.
- Problemas de resolução de nomes.

## <a name="user-action"></a>Ação do usuário

Examine as seções a seguir para obter as ações que você pode executar para cada uma das diferentes causas mencionadas acima.

### <a name="verify-the-login-you-are-trying-to-add"></a>Verifique o logon que você está tentando adicionar

1. Verifique se o logon do Windows ainda existe no domínio. O administrador de rede pode ter removido o logon do Windows por motivos específicos, e talvez você não possa permitir esse acesso de logon ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
1. Verifique se os nomes de domínio e de logon foram escritos corretamente e se você está usando o seguinte formato: `Domain\User`
1. Se o logon existir e estiver correto e você ainda receber o erro, continue com as seções a seguir deste artigo.

### <a name="verify-if-the-domain-controller-is-available"></a>Verificar se o controlador de domínio está disponível

Você poderá receber o erro 15401 quando o controlador do domínio em que reside o logon (o mesmo ou um domínio diferente) não estiver disponível por algum motivo.

Se o logon estiver em um domínio diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], verifique se existem relações de confiança corretas entre os domínios.

Verifique se o controlador de domínio do logon está acessível usando o comando ping no computador que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Verifique o endereço IP e o nome do controlador de domínio.

### <a name="verify-the-domain-name-for-local-accounts"></a>Verificar o nome de domínio para contas locais

Contas locais (não de domínio) exigem tratamento especial. Se você estiver tentando adicionar uma conta local no computador local que executa o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use BUILTIN como o nome de domínio.

### <a name="check-for-name-resolution-issues"></a>Verificar se há problemas de resolução de nomes

Caso tenha problemas para resolver o nome de um computador que está envolvido na adição do logon ou do grupo, você poderá receber o erro 15401.

Verifique se o mecanismo de resolução de nomes (como o WINS, o DNS, o HOSTS ou o LMHOSTS) está configurado corretamente.

## <a name="see-also"></a>Consulte também

- [Testar um canal entre o computador local e o respectivo domínio](/powershell/module/microsoft.powershell.management/test-computersecurechannel#example-1--test-a-channel-between-the-local-computer-and-its-domain)
- [LogonSessions v1.4](/sysinternals/downloads/logonsessions)
- [sp_change_users_login (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-change-users-login-transact-sql)
