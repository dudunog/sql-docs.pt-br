---
title: Quais são as novidades nas Extensões de Linguagem do SQL Server?
titleSuffix: ''
description: Conheça as novidades das Extensões de Linguagem do SQL Server.
author: dphansen
ms.author: davidph
ms.date: 11/05/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: language-extensions
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b52daf4ad0e789dc1508b5903cc95a92c39e0929
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921044"
---
# <a name="whats-new-in-sql-server-language-extensions"></a>Quais são as novidades nas Extensões de Linguagem do SQL Server?
[!INCLUDE[sqlserver](../includes/applies-to-version/sqlserver.md)]

As funcionalidades da [Extensão de Linguagem](language-extensions-overview.md) são adicionadas ao SQL Server em cada versão conforme continuamos expandindo, estendendo e aprofundando a integração entre linguagens externas e a plataforma de dados. 

## <a name="new-in-sql-server-2019"></a>Novidades do SQL Server 2019 

Esta versão adiciona o suporte para Extensões de Linguagem no SQL Server. Para obter mais informações sobre todos os recursos desta versão, confira [Novidades do SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md) e [Notas sobre a versão do SQL Server 2019](../sql-server/sql-server-ver15-release-notes.md).

- O Runtime do Java padrão no Windows e Linux é o Open Zulu JRE e é incluído com a [instalação das Extensões de Linguagem do SQL Server no Windows](install/install-sql-server-language-extensions-on-windows.md) e a [instalação das Extensões de Linguagem do SQL Server no Linux](../linux/sql-server-linux-setup-language-extensions.md).
- [Tipos de dados Java](how-to/java-to-sql-data-types.md) com suporte.
- [CREATE EXTERNAL LANGUAGE](../t-sql/statements/create-external-language-transact-sql.md) para registrar a linguagem externa (por exemplo, Java) no SQL Server.
- [SDK de Extensibilidade da Microsoft para Java](how-to/extensibility-sdk-java-sql-server.md).
- No Windows e no Linux, o código Java pode ser acessado em uma biblioteca externa usando a instrução [CREATE EXTERNAL LIBRARY (Transact-SQL)](../t-sql/statements/create-external-library-transact-sql.md). Saiba mais: [Como chamar Java do SQL Server](how-to/call-java-from-sql.md).
- [Extensão da linguagem Java](language-extensions-overview.md) no Windows e Linux. Você pode disponibilizar o código Java compilado para o SQL Server atribuindo permissões e definindo o caminho. Os aplicativos cliente com acesso ao SQL Server podem usar dados e executar seu código chamando [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql), o mesmo procedimento usado para a integração do R e Python nos Serviços de Machine Learning do SQL Server.

## <a name="next-steps"></a>Próximas etapas

+ Instalar [Extensões de Linguagem do SQL Server no Windows](install/install-sql-server-language-extensions-on-windows.md) ou [no Linux](../linux/sql-server-linux-setup-language-extensions.md)
