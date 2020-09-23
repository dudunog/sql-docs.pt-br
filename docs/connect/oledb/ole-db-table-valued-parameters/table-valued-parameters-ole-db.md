---
title: Parâmetros com valor de tabela (Driver do OLE DB)
description: Estes artigos descrevem o suporte para parâmetros com valor de tabela no Driver do OLE DB para SQL Server, incluindo a criação de conjunto de linhas de parâmetro e a descoberta do tipo de parâmetro.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c49b476492d2296ce1224f935644dca650aefbf
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859873"
---
# <a name="table-valued-parameters-ole-db"></a>Parâmetros com valor de tabela (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Esta seção descreve o suporte a parâmetros com valor de tabela no Driver do OLE DB para SQL Server. Para obter informações gerais adicionais, confira [Parâmetros com valor de tabela &#40;Driver do OLE DB para SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md). Para ver uma amostra, confira [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md).  
  
## <a name="remarks"></a>Comentários  
 Atualmente, você pode enviar dados de várias linhas ao servidor como parâmetros para um procedimento com conjuntos de parâmetros (o parâmetro DBPARAMS em **ICommand::Execute**). Com conjuntos de parâmetros, todo elemento do conjunto tem que ser enviado ao servidor em uma solicitação RPC (chamada de procedimento remoto) separada. Os parâmetros com valor de tabela fornecem uma funcionalidade semelhante, mas interagem melhor com o servidor. Isso reduz o número de solicitações RPC e habilita operações baseadas em conjunto no servidor.  
  
 Os parâmetros de valor de tabela são compatíveis com o Driver do OLE DB para SQL Server como objetos **Rowset** do OLE DB. Qualquer objeto **Rowset** pode ser fornecido pelo consumidor (ou seja, o aplicativo cliente que usa o OLE DB Driver for SQL Server) como um espaço reservado para parâmetros com valor de tabela. Os parâmetros com valor de tabela são tratados como os outros tipos de parâmetro do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O Driver do OLE DB para SQL Server fornece interfaces de criação, descoberta, especificação, associação e de esquema.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Criação do conjunto de linhas do parâmetro com valor de tabela](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [Descoberta do tipo de parâmetro com valor de tabela](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [Executando comandos que contêm parâmetros com valor de tabela](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [Inserindo dados em parâmetros com valor de tabela](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [Conjuntos de linhas de esquema alterados para parâmetros com valor de tabela de OLE DB](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela OLE DB](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela OLE DB &#40;Métodos&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [Suporte ao tipo de parâmetro com valor de tabela do OLE DB &#40;Propriedades&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no OLE DB Driver for SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
