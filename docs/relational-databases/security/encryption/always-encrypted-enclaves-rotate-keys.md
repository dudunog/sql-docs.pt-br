---
description: Girar chaves habilitadas para enclave
title: Rotação | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.reviewer: vanto
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 8ef5e2e3cbf4e00619aeb4b0d1643f0d07100aad
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534312"
---
# <a name="rotate-enclave-enabled-keys"></a>Girar chaves habilitadas para enclave

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

No Always Encrypted, uma rotação de chave é um processo de substituição de uma chave mestra de coluna ou uma chave de criptografia de coluna existente por uma nova chave. Este artigo descreve casos de uso e considerações para a rotação de chaves específicas do [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) quando a chave inicial e/ou a (nova) chave de destino é uma chave habilitada para enclave. Para obter diretrizes gerais e processos para gerenciar as chaves do Always Encrypted, confira [Visão geral do gerenciamento de chaves do Always Encrypted](overview-of-key-management-for-always-encrypted.md). 

Talvez seja necessário girar uma chave por motivos de segurança ou conformidade. Por exemplo, se uma chave é comprometida ou se as políticas da sua organização exigem a substituição das chaves periodicamente. Além disso, o Always Encrypted com a rotação de chaves de enclaves seguros fornece uma maneira de habilitar ou desabilitar a funcionalidade do enclave seguro do servidor para as colunas criptografadas.

- Ao substituir uma chave que não está habilitada para enclave por uma chave habilitada para enclave, você desbloqueia a funcionalidade do enclave seguro para consultas em colunas que estão protegidas com a chave. Para obter mais informações, confira [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md).
- Ao substituir uma chave habilitada para enclave por uma chave que não está habilitada para enclave, você desabilita a funcionalidade do enclave seguro para consultas em colunas que estão protegidas com a chave.

Se você estiver girando uma chave apenas por motivos de segurança/conformidade e não para habilitar ou desabilitar computações de enclave para as colunas, verifique se a chave de destino tem a mesma configuração em relação aos enclaves que a chave de origem. Por exemplo, se a chave de origem está habilitada para enclave, a chave de destino também deve estar habilitada para enclave.

As etapas abaixo incluem links para artigos detalhados, dependendo do cenário de rotação:

1. Provisionar uma nova chave (uma chave mestra de coluna ou uma chave de criptografia de coluna).
    - Para provisionar uma nova chave habilitada para enclave, confira [Provisionar chaves habilitadas para enclave](always-encrypted-enclaves-provision-keys.md).
    - Para provisionar uma chave que não está habilitada para enclave, confira [Provisionar chaves do Always Encrypted usando o SQL Server Management Studio](configure-always-encrypted-keys-using-ssms.md) e [Provisionar chaves do Always Encrypted usando o PowerShell](configure-always-encrypted-keys-using-powershell.md).
2. Substitua uma chave existente pela nova chave.
    - Se você estiver girando uma chave de criptografia de coluna e a chave de origem e a chave de destino estiverem habilitadas para enclave, execute a rotação (que envolve a nova criptografia dos dados) in-loco. Para obter mais informações, confira [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md).
    - Para obter etapas detalhadas para girar as chaves, confira [Girar chaves do Always Encrypted usando o SQL Server Management Studio](rotate-always-encrypted-keys-using-ssms.md) e [Girar chaves do Always Encrypted usando o PowerShell](rotate-always-encrypted-keys-using-powershell.md).

## <a name="next-steps"></a>Próximas etapas

- [Executar instruções Transact-SQL usando os enclaves seguros](always-encrypted-enclaves-query-columns.md)
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md)
- [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)  

## <a name="see-also"></a>Consulte Também  
- [Gerenciar chaves para Always Encrypted com enclaves seguros](always-encrypted-enclaves-manage-keys.md)