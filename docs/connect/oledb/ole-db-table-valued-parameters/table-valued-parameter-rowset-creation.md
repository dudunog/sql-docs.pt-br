---
title: Criação do conjunto de linhas do parâmetro com valor de tabela | Microsoft Docs
description: Criação do conjunto de linhas do parâmetro com valor de tabela estático e dinâmico
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 00103e02efe284e9c5d60e2f251f8bc28646a30d
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86003343"
---
# <a name="table-valued-parameter-rowset-creation"></a>Criação do conjunto de linhas do parâmetro com valor de tabela
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Embora os consumidores possam fornecer qualquer objeto do conjunto de linhas a parâmetros com valor de tabela, objetos do conjunto de linhas típicos são implementados com relação a armazenamentos de dados de back-end e, portanto, fornecem desempenho limitado. Por isso, o OLE DB Driver for SQL Server permite que os consumidores criem um objeto de conjunto de linhas especializado sobre os dados da memória. Esse objeto do conjunto de linhas especial na memória é um novo objeto COM denominado conjunto de linhas do parâmetro com valor de tabela. Ele fornece funcionalidade semelhante para conjuntos de parâmetro.  
  
 Os objetos do conjunto de linhas do parâmetro com valor de tabela são criados explicitamente pelo consumidor para parâmetros de entrada por meio de várias interfaces no nível da sessão. Há uma instância de um objeto do conjunto de linhas de parâmetro com valor de tabela por parâmetro com valor de tabela. O consumidor pode criar os objetos do conjunto de linhas do parâmetro com valor de tabela fornecendo informações de metadados já conhecidas (cenário estático) ou descobrindo-as por meio das interfaces do provedor (cenário dinâmico). As seções a seguir descrevem estes dois cenários.  
  
## <a name="static-scenario"></a>Cenário estático  
 Quando as informações de tipo são conhecidas, o consumidor usa ITableDefinitionWithConstraints::CreateTableWithConstraints para criar uma instância de um conjunto de linhas do parâmetro com valor de tabela que corresponda a um parâmetro com valor de tabela.  
  
 O campo *guid* (parâmetro *pTableID*) contém a GUID especial (CLSID_ROWSET_TVP). O membro *pwszName* contém o nome do tipo de parâmetro com valor de tabela para o qual o consumidor deseja criar uma instância. O campo *eKind* será definido como DBKIND_GUID_NAME. Esse nome é obrigatório quando a instrução é SQL ad hoc; o nome é opcional se é uma chamada de procedimento.  
  
 Para agregação, o consumidor transmite o parâmetro *pUnkOuter* com o controlador IUnknown.  
  
 As propriedades do objeto de conjunto de linhas de parâmetro com valor de tabela são somente leitura e, portanto, não é esperado que o consumidor defina propriedades em *rgPropertySets*.  
  
 Para o membro *rgPropertySets* de cada estrutura DBCOLUMNDESC, o consumidor pode especificar propriedades adicionais para cada coluna. Essas propriedades pertencem ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN. Elas permitem que você especifique as configurações computadas e padrão de cada coluna. Elas também dão suporte a propriedades de coluna existentes, como nulidade e identidade.  
  
 Para recuperar informações correspondentes de um objeto do conjunto de linhas do parâmetro com valor de tabela, o consumidor usa IRowsetInfo::GetProperties.  
  
 Para recuperar informações sobre o status nulo, exclusivo, computado e de atualização de cada coluna, o consumidor pode usar IColumnsRowset::GetColumnsRowset ou IColumnsInfo::GetColumnInfo. Esses métodos fornecem informações detalhadas sobre cada coluna do conjunto de linhas do parâmetro com valor de tabela.  
  
 O consumidor especifica o tipo de cada coluna do parâmetro com valor de tabela. Isso é semelhante à forma como as colunas são especificadas quando uma tabela é criada no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. O consumidor obtém um objeto do conjunto de linhas do parâmetro com valor de tabela do Driver do OLE DB para SQL Server por meio do parâmetro de saída *ppRowset*.  
  
## <a name="dynamic-scenario"></a>Cenário dinâmico  
 Quando o consumidor não tiver informações de tipo, deve usar IOpenRowset::OpenRowset para criar uma instância dos objetos do conjunto de linhas do parâmetro com valor de tabela. O consumidor deve fornecer ao provedor somente o nome do tipo.  
  
 Nesse cenário, o provedor obtém as informações de tipo sobre um objeto do conjunto de linhas do parâmetro com valor de tabela do servidor em nome do consumidor.  
  
 Os parâmetros *pTableID* e *pUnkOuter* devem ser definidos como no cenário estático. O OLE DB Driver for SQL Server obtém então as informações de tipo (informações e restrições da coluna) do servidor e retorna um objeto do conjunto de linhas do parâmetro com valor de tabela por meio do parâmetro *ppRowset*. Essa operação exige a comunicação com o servidor e, portanto, não tem desempenho tão bom quanto no cenário estático. O cenário dinâmico só funciona com chamadas de procedimento com parâmetros.  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
