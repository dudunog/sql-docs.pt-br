---
title: BLOBs e objetos OLE (Driver do OLE DB) | Microsoft Docs
description: BLOBs e objetos OLE
ms.custom: ''
ms.date: 05/25/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- BLOBs, OLE objects
- BLOBs
- storage object [OLE DB]
- OLE DB Driver for SQL Server, BLOBs
- large data, OLE objects
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 54f8b4c38c22bcb32b039d9f0f0887c298051302
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942757"
---
# <a name="blobs-and-ole-objects"></a>BLOBs e objetos OLE
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O Driver do OLE DB para SQL Server expõe a interface **ISequentialStream** para dar suporte ao acesso do consumidor aos tipos de dados **ntext**, **text**<a href="#text_note"><sup>**1**</sup></a>, **image**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** e xml do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como BLOBs (objetos binários grandes). O método **Read** em **ISequentialStream** permite que o consumidor recupere muitos dados em partes gerenciáveis.

 <b id="text_note">[1]:</b> o uso da interface ISequentialStream para inserir dados codificados em UTF-8 em uma coluna de texto herdada só é limitado a servidores que dão suporte a UTF-8. Uma tentativa de executar esse cenário ao ter como direcionamento um servidor que não dá suporte a UTF-8 fará com que o driver envie a seguinte mensagem de erro: "*Streaming sem suporte no tipo de coluna selecionado*".

 Para obter um exemplo que demonstra esse recurso, confira [Definir &#40;OLE DB&#41; de dados grandes](../../oledb/ole-db-how-to/set-large-data-ole-db.md).  
  
 O OLE DB Driver for SQL Server pode usar uma interface **IStorage** implementada pelo consumidor quando o consumidor fornece o ponteiro de interface em um acessador associado para modificação de dados.  
  
 Para tipos de dados de valor grande, o OLE DB Driver for SQL Server verifica as suposições de tamanho de tipo em interfaces **IRowset** e DDL. As colunas que têm tipos de dados **varchar**, **nvarchar** e **varbinary** e o tamanho máximo definido como ilimitado serão representadas como ISLONG pelos conjuntos de linhas do esquema e pelas interfaces que retornam tipos de dados de coluna.  
  
 O OLE DB Driver for SQL Server expõe os tipos **varchar(max)** , **varbinary(max)** e **nvarchar(max)** como DBTYPE_STR, DBTYPE_BYTES e DBTYPE_WSTR, respectivamente.  
  
 Para trabalhar com esses tipos, um aplicativo tem as seguintes opções:  
  
-   Associar como o tipo (DBTYPE_STR, DBTYPE_BYTES, DBTYPE_WSTR). Se o buffer não for grande o suficiente, ocorrerá truncamento, exatamente como para esses tipos em versões anteriores (embora agora haja valores maiores disponíveis).  
  
-   Associar como o tipo e também especificar DBTYPE_BYREF.  
  
-   Associar como DBTYPE_IUNKNOWN e usar streaming.  
  
 Se associado a DBTYPE_IUNKNOWN, é usada a funcionalidade de fluxo ISequentialStream. O Driver do OLE DB para SQL Server dá suporte à associação de parâmetros de saída como DBTYPE_IUNKNOWN para tipos de dados de valor grande. Isso é para dar suporte a cenários em que um procedimento armazenado retorna esses tipos de dados como valores retornados, que serão retornados como DBTYPE_IUNKNOWN ao cliente.  
  
## <a name="storage-object-limitations"></a>Limitações de objetos de armazenamento  
  
-   O Driver do OLE DB para SQL Server pode dar suporte apenas a um objeto de armazenamento aberto. As tentativas de abrir mais de um objeto de armazenamento (para obter uma referência em mais de um ponteiro da interface **ISequentialStream**) retornam DBSTATUS_E_CANTCREATE.  
  
-   No OLE DB Driver for SQL Server, o valor padrão da propriedade somente leitura DBPROP_BLOCKINGSTORAGEOBJECTS é VARIANT_TRUE. Portanto, se um objeto de armazenamento estiver ativo, alguns métodos (diferentes dos métodos nos objetos de armazenamento) falharão com E_UNEXPECTED.  
  
-   O tamanho dos dados apresentados por um objeto de armazenamento implementado pelo consumidor precisa ser conhecido pelo OLE DB Driver for SQL Server quando o acessador de linha que referencia o objeto de armazenamento é criado. O consumidor deve associar um indicador de comprimento na estrutura DBBINDING usada para a criação do acessador.  
  
-   Se uma linha contiver mais de um único valor de dados grande e DBPROP_ACCESSORDER não for DBPROPVAL_AO_RANDOM, o consumidor precisará usar um conjunto de linhas com suporte do cursor do OLE DB Driver for SQL Server para recuperar dados de linha ou processar todos os valores de dados grandes antes de recuperar outros valores de linha. Se DBPROP_ACCESSORDER for DBPROPVAL_AO_RANDOM, o OLE DB Driver for SQL Server armazenará em cache todos os tipos de dados xml como BLOBs (objetos binários grandes), de forma que possam ser acessados em qualquer ordem.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Obtendo dados grandes](../../oledb/ole-db-blobs/getting-large-data.md)  
  
-   [Configurando dados grandes](../../oledb/ole-db-blobs/setting-large-data.md)  
  
-   [Suporte de streaming para parâmetros de saída BLOB](../../oledb/ole-db-blobs/streaming-support-for-blob-output-parameters.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Programação no OLE DB Driver for SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)        
 [Usando tipos de valor grande](../../oledb/features/using-large-value-types.md)  
  
  
