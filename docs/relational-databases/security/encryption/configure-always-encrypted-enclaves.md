---
title: Configurar e usar o Always Encrypted com enclaves seguros | Microsoft Docs
description: Saiba como configurar e usar o Always Encrypted com enclaves seguros no SQL Server e no Banco de Dados SQL do Azure, que permite uma funcionalidade mais avançada em dados confidenciais.
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 481493a50fdefc22f6eb4d77feb13cfc4848388d
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534645"
---
# <a name="configure-and-use-always-encrypted-with-secure-enclaves"></a>Configurar e usar o Always Encrypted com enclaves seguros 

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) estende o recurso [Always Encrypted](always-encrypted-database-engine.md) existente para habilitar funcionalidades mais avançadas em dados confidenciais mantendo a confidencialidade desses dados. Este artigo lista tarefas comuns para configurar e usar o recurso.

Para obter tutoriais que mostram como começar rapidamente a usar o Always Encrypted com enclaves seguros, confira:

- [Tutorial: Introdução ao Always Encrypted com enclaves seguros no SQL Server](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros no Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)

## <a name="set-up-the-secure-enclave-and-attestation"></a>Configurar o enclave seguro e o atestado

Para usar o Always Encrypted com enclaves seguros, configure seu ambiente para garantir que o enclave seguro esteja disponível para o banco de dados. Você também precisará configurar o [atestado de enclave](always-encrypted-enclaves.md#secure-enclave-attestation). 

O processo para configurar seu ambiente depende de você estar usando o [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] ou o [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

### <a name="set-up-the-secure-enclave-and-attestation-in-ssnoversion-md"></a>Configurar o enclave seguro e o atestado no [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]

Para obter detalhes, confira os seguintes artigos:
- [Planejar o atestado do Serviço Guardião de Host](./always-encrypted-enclaves-host-guardian-service-plan.md)
- [Implantar o Serviço Guardião de Host para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]](./always-encrypted-enclaves-host-guardian-service-deploy.md)
- [Registrar o computador no Serviço Guardião de Host](./always-encrypted-enclaves-host-guardian-service-register.md)
- [Configurar o enclave seguro no SQL Server](always-encrypted-enclaves-configure-enclave-type.md)

### <a name="set-up-the-secure-enclave-and-attestation-in-sssdsfull"></a>Configurar o enclave seguro e o atestado no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]

Para obter detalhes, confira os seguintes artigos:
- [Planejar o atestado e os enclaves Intel SGX no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]](/azure/azure-sql/database/always-encrypted-enclaves-sqldbmi-plan)
- [Habilitar o SGX Intel para seu Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-sqldbmi-enable-sgx)
- [Configurar o Atestado do Azure para o servidor lógico do Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-sqldbmi-configure-attestation)

## <a name="manage-keys-for-always-encrypted-with-secure-enclaves"></a>Gerenciar chaves para Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Gerenciar chaves para Always Encrypted com enclaves seguros – visão geral](always-encrypted-enclaves-manage-keys.md)
- [Provisionar chaves habilitadas para enclave](always-encrypted-enclaves-provision-keys.md)
- [Girar chaves habilitadas para enclave](always-encrypted-enclaves-rotate-keys.md)

## <a name="configure-columns-with-always-encrypted-with-secure-enclaves"></a>Configurar colunas com o Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros – visão geral](always-encrypted-enclaves-configure-encryption.md)
- [Configurar criptografia de coluna in-loco com Transact-SQL](always-encrypted-enclaves-configure-encryption-tsql.md)
- [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md)

## <a name="run-transact-sql-statements-using-secure-enclaves"></a>Executar instruções Transact-SQL usando os enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Executar instruções Transact-SQL usando os enclaves seguros](always-encrypted-enclaves-query-columns.md)
- [Solução de problemas comuns do Always Encrypted com enclaves seguros](always-encrypted-enclaves-troubleshooting.md)

## <a name="create-and-use-indexes-on-enclave-enabled-columns"></a>Criar e usar índices em colunas habilitadas para enclave
Confira os seguintes artigos para obter detalhes:
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)
  
## <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Desenvolver aplicativos usando o Always Encrypted com enclaves seguros
Confira os seguintes artigos para obter detalhes:
- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)
