---
title: Transações e simultaneidade
description: Descreve como usar o Provedor de Dados Microsoft SqlClient para SQL Server com transações e simultaneidade.
ms.date: 11/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: a30a3d3184c411fc0b54c0e26330a8fb138ffdae
ms.sourcegitcommit: 2add15a99df7b85d271adb261523689984dfd134
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97051238"
---
# <a name="transactions-and-concurrency"></a>Transações e simultaneidade

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Uma transação consiste em um único comando ou em um grupo de comandos executados como um pacote. As transações permitem que você combine várias operações em uma única unidade de trabalho. Se uma falha ocorrer em determinado ponto na transação, todas as atualizações poderão ser revertidas para o estado em vigor antes da transação.

Uma transação deve estar de acordo com as propriedade ACID — atomicidade, consistência, isolamento e durabilidade — para garantir a consistência dos dados. A maioria dos sistemas de banco de dados relacional, como o Microsoft SQL Server, oferece suporte a transações fornecendo recursos de bloqueio, registro e gerenciamento de transação sempre que um aplicativo cliente executa uma operação de atualização, inserção ou exclusão.

> [!NOTE]
> As transações que envolvem vários recursos podem reduzir a simultaneidade se os bloqueios forem mantidos muito longos. Portanto, mantenha as transações curtas, o quanto possível.  

Se uma transação envolver várias tabelas no mesmo banco de dados ou servidor, as transações explícitas em procedimentos armazenados geralmente apresentarão um melhor desempenho. Você pode criar transações em procedimentos armazenados do SQL Server usando as instruções Transact-SQL `BEGIN TRANSACTION`, `COMMIT TRANSACTION` e `ROLLBACK TRANSACTION`. Para obter mais informações, consulte os Manuais Online do SQL Server.

As transações que envolvem diferentes gerenciadores de recursos, como uma transação entre o SQL Server e o Oracle, exigem uma transação distribuída.

## <a name="in-this-section"></a>Nesta seção

 [Transações locais](local-transactions.md)  
 Demonstra como executar transações em um banco de dados.  
  
 [Transações distribuídas](distributed-transactions.md)  
 Descreve como executar transações distribuídas no ADO.NET.  
  
 [Integração de System.Transactions com SQL Server](system-transactions-integration-with-sql-server.md)  
 Descreve a integração do <xref:System.Transactions> com o SQL Server para trabalhar com transações distribuídas.  
  
 [Simultaneidade otimista](optimistic-concurrency.md) Descreve a simultaneidade otimista e pessimista e como você pode testar violações de simultaneidade.  

## <a name="see-also"></a>Confira também

- [Conceitos básicos da transação](/dotnet/framework/data/transactions/transaction-fundamentals)
- [Como se conectar à fonte de dados](connecting-to-data-source.md)
- [Comandos e parâmetros](commands-parameters.md)
- [DataAdapters e DataReaders](dataadapters-datareaders.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
