---
title: Configurar o enclave seguro no SQL Server
description: Configure o enclave seguro para Always Encrypted com enclaves seguros no SQL Server.
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: f2aa24e3ebd335251ad2721444e9f9d8645ef221
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534859"
---
# <a name="configure-the-secure-enclave-in-sql-server"></a>Configurar o enclave seguro no SQL Server

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Para usar o [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) no SQL Server, configure sua instância para inicializar o enclave seguro durante a inicialização. Por padrão, o SQL Server não inicializa o enclave seguro. Você pode alterar isso definindo a opção de configuração de servidor de **tipo de enclave de criptografia de coluna** para o valor que representa um tipo de enclave válido para o seu ambiente.

> [!NOTE]
> Essa função responsável por configurar o enclave seguro é o DBA. Confira [Funções e responsabilidades ao configurar o atestado com o HGS](always-encrypted-enclaves-host-guardian-service-plan.md#roles-and-responsibilities-when-configuring-attestation-with-hgs).

O tipo de enclave compatível com [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] é a VBS (segurança baseada em virtualização). Antes de configurar o tipo de enclave VBS, recomendamos que você configure o atestado com o HGS (Serviço Guardião de Host) para o computador que hospeda sua instância. Para começar a usar o HGS, confira [Planejar o atestado com o Serviço Guardião de Host](always-encrypted-enclaves-host-guardian-service-plan.md). A configuração do atestado também permite a segurança baseada em virtualização, que é necessária para que um enclave VBS seja inicializado corretamente. Para obter mais informações, confira [Verificar se a segurança baseada em virtualização está em execução](always-encrypted-enclaves-host-guardian-service-register.md#step-2-verify-virtualization-based-security-is-running).

Para obter instruções detalhadas sobre como configurar o tipo de enclave, confira [Configurar o tipo de enclave para a opção de configuração de servidor do Always Encrypted](../../../database-engine/configure-windows/configure-column-encryption-enclave-type.md).

## <a name="next-steps"></a>Próximas etapas

 [Gerenciar chaves para Always Encrypted com enclaves seguros](always-encrypted-enclaves-manage-keys.md)

## <a name="see-also"></a>Consulte Também  
 
 [Opções de configuração do servidor (SQL Server)](../../../database-engine/configure-windows/server-configuration-options-sql-server.md)
