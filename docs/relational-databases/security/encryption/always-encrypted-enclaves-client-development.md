---
description: Desenvolver aplicativos usando o Always Encrypted com enclaves seguros
title: Desenvolver aplicativos usando o Always Encrypted com enclaves seguros | Microsoft Docs
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
dev_langs:
- CSharp
ms.assetid: 9595eb66-284c-4474-828f-8961a05ce989
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 18a841153ba4b9f99c1b1d083950ca106f4ce765
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534625"
---
# <a name="develop-applications-using-always-encrypted-with-secure-enclaves"></a>Desenvolver aplicativos usando o Always Encrypted com enclaves seguros
[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) estende o [Always Encrypted](always-encrypted-database-engine.md) para habilitar uma funcionalidade mais rica das consultas de aplicativo em colunas de banco de dados confidenciais criptografadas. Ele aproveita as tecnologias de enclave seguro para permitir que o executor da consulta em [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] delegue cálculos em colunas criptografadas a um enclave seguro dentro do processo de [!INCLUDE[ssde-md](../../../includes/ssde-md.md)].

## <a name="prerequisites"></a>Pré-requisitos

- A instância do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] ou o banco de dados e o servidor do [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] precisam ser configurados corretamente para dar suporte aos enclaves e ao atestado. Para obter mais informações, confira [Configurar o atestado e enclave seguro](configure-always-encrypted-enclaves.md#set-up-the-secure-enclave-and-attestation).
- Você precisará obter uma URL de atestado para seu ambiente do administrador de serviços de atestado.

  - Se você estiver usando o [!INCLUDE[ssnoversion-md](../../../includes/ssnoversion-md.md)] e o HGS (Serviço Guardião de Host), confira [Determinar e compartilhar a URL de atestado do HGS](../../../relational-databases/security/encryption/always-encrypted-enclaves-host-guardian-service-deploy.md#step-6-determine-and-share-the-hgs-attestation-url).
  - Se você estiver usando o [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] e o Atestado do Microsoft Azure, confira [Determinar a URL de atestado para a política de atestado](/azure-sql/database/always-encrypted-enclaves-configure-attestation#determine-the-attestation-url-for-your-attestation-policy).

- Seu aplicativo precisa usar uma versão de driver de cliente do SQL que dê suporte a enclaves seguros. Confira as seções abaixo para obter mais detalhes.

- Você precisará configurar um protocolo e uma URL de atestado para uma conexão de banco de dados. Os detalhes de como configurar o protocolo e a URL de atestado dependem do driver de cliente usado.

## <a name="client-drivers-for-always-encrypted-with-secure-enclaves"></a>Drivers de cliente do Always Encrypted com enclaves seguros

Para desenvolver aplicativos usando o Always Encrypted com enclaves seguros, você precisa de uma versão do driver de cliente do SQL que dê suporte a enclaves seguros. O driver de cliente desempenha a seguinte função importante:

- Antes de enviar uma consulta que usa um enclave seguro para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para execução, o driver inicia o atestado do enclave para verificar se o enclave seguro é confiável e pode ser usado com segurança para processar dados confidenciais. Para obter mais informações sobre o atestado, confira [Atestado de enclave seguro](always-encrypted-enclaves.md#secure-enclave-attestation).
- Depois que o atestado for bem sucedido, o driver de cliente estabelecerá uma sessão segura com o enclave negociando um segredo compartilhado.
- O driver usa o segredo compartilhado para criptografar as chaves de criptografia de coluna de que o enclave precisará para processar a consulta e envia as chaves para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], que as encaminha para o enclave seguro que descriptografa as chaves. 
- Por fim, o driver envia a consulta para execução, i que dispara cálculos dentro do enclave seguro.

## <a name="next-steps"></a>Próximas etapas

Os drivers de cliente a seguir são suporte ao Always Encrypted com enclaves seguros:

- Provedor de Dados do Microsoft .NET para SQL Server no .NET Framework 4.6 ou superior e no .NET Core 2.1 ou superior. 
    - Para obter mais informações, confira [Como usar o Always Encrypted com o Provedor de Dados do Microsoft .NET para SQL Server](../../../connect/ado-net/sql/sqlclient-support-always-encrypted.md).
    - Para obter um tutorial passo a passo, confira [Tutorial: como desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros](../../../connect/ado-net/sql/tutorial-always-encrypted-enclaves-develop-net-apps.md).
    - Confira também [Exemplo que demonstra o uso do provedor do Azure Key Vault e o Always Encrypted com enclaves seguros](../../../connect/ado-net/sql/azure-key-vault-enclave-example.md).
- Microsoft ODBC Driver for SQL Server, versão 17.4 ou acima. 
    - Para obter mais informações, veja [Como usar Always Encrypted com o driver ODBC do Windows](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md). 
    - Para obter informações sobre como habilitar computações de enclave para uma conexão de banco de dados usando o ODBC, confira a seção [Como habilitar o Always Encrypted com enclaves seguros](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#enabling-always-encrypted-with-secure-enclaves).
- Microsoft ODBC Driver para SQL Server, versão 8.2 ou superior.
    - Para obter mais informações, confira [Como usar o Always Encrypted com enclaves seguros com o driver ODBC](../../../connect/jdbc/using-always-encrypted-with-secure-enclaves-with-the-jdbc-driver.md)
- Provedor de Dados do .NET Framework para SQL Server no .NET Framework 4.7.2 ou acima. 
    - Para obter mais informações, confira [Usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](../../../relational-databases/security/encryption/develop-using-always-encrypted-with-net-framework-data-provider.md).
    - Para obter um tutorial passo a passo, confira [Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros](../tutorial-always-encrypted-enclaves-develop-net-framework-apps.md)

## <a name="see-also"></a>Confira também

- [Solução de problemas comuns do Always Encrypted com enclaves seguros](always-encrypted-enclaves-troubleshooting.md)
