---
description: Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted habilitado com Enclaves Seguros
title: Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted habilitado com Enclaves Seguros | Microsoft Docs
ms.custom: ''
ms.date: 11/17/2020
ms.reviewer: v-kaywon
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: karinazhou
ms.author: v-jizho2
ms.openlocfilehash: 548c5e8716f4ba15de675de856a5e5bd8206da35
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534482"
---
# <a name="example-demonstrating-use-of-azure-key-vault-provider-with-always-encrypted-enabled-with-secure-enclaves"></a>Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted habilitado com Enclaves Seguros

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

[!INCLUDE [appliesto-netfx-netcore-xxxx-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

Este exemplo demonstra o uso do Provedor do Azure Key Vault ao acessar colunas criptografadas.

[!code-csharp [Azure Key Vault Provider with Enclave Example#1](~/../sqlclient/doc/samples/AzureKeyVaultProviderWithEnclaveProviderExample.cs#1)]

> [!NOTE]
> - Para usar Always Encrypted com enclaves seguros para o aplicativo .NET Standard, é necessário o **Microsoft.Data.SqlClient** versão 2.1.0 ou posterior. A versão do .NET Standard com suporte é a 2.1 ou posterior. 
>
> - Para usar Always Encrypted com enclaves seguros no Linux ou macOS, é necessário o **Microsoft.Data.SqlClient** versão 2.1.0 ou posterior.

## <a name="see-also"></a>Veja também

- [Exemplo que demonstra o uso do provedor do Azure Key Vault com Always Encrypted](azure-key-vault-example.md)
- [Tutorial: Desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros](tutorial-always-encrypted-enclaves-develop-net-apps.md)
- [Como usar o Always Encrypted com o Provedor de Dados do Microsoft .NET para SQL Server](sqlclient-support-always-encrypted.md)
