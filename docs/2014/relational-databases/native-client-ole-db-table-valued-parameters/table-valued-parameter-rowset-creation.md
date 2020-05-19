---
title: Criação do conjunto de linhas do parâmetro com valor de tabela | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters, rowset creation
ms.assetid: ffe213ca-cc0e-465e-b31c-a8272324c4fe
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: eee3452c109bcd519cb24ba96b621ec25c0110df
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704591"
---
# <a name="table-valued-parameter-rowset-creation"></a>Criação do conjunto de linhas do parâmetro com valor de tabela
  Embora os consumidores possam fornecer qualquer objeto do conjunto de linhas a parâmetros com valor de tabela, objetos do conjunto de linhas típicos são implementados com relação a armazenamentos de dados de back-end e, portanto, fornecem desempenho limitado. Por isso, o provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client permite que os consumidores criem um objeto de conjunto de linhas especializado sobre os dados da memória. Esse objeto de conjunto de linhas em memória especial é um novo objeto COM chamado conjunto de linhas de parâmetro COM valor de tabela. Ele fornece funcionalidade semelhante para conjuntos de parâmetro.  
  
 Os objetos do conjunto de linhas do parâmetro com valor de tabela são criados explicitamente pelo consumidor para parâmetros de entrada por meio de várias interfaces no nível da sessão. Há uma instância de um objeto do conjunto de linhas do parâmetro com valor de tabela por parâmetro com valor de tabela. O consumidor pode criar os objetos do conjunto de linhas do parâmetro com valor de tabela fornecendo informações de metadados já conhecidas (cenário estático) ou descobrindo-as por meio das interfaces do provedor (cenário dinâmico). As seções a seguir descrevem estes dois cenários.  
  
## <a name="static-scenario"></a>Cenário estático  
 Quando as informações de tipo são conhecidas, o consumidor usa ITableDefinitionWithConstraints::CreateTableWithConstraints para criar uma instância de um conjunto de linhas do parâmetro com valor de tabela que corresponda a um parâmetro com valor de tabela.  
  
 O campo *guid* (parâmetro *pTableID*) contém a GUID especial (CLSID_ROWSET_TVP). O membro *pwszName* contém o nome do tipo de parâmetro com valor de tabela para o qual o consumidor deseja criar uma instância. O campo *eKind* será definido como DBKIND_GUID_NAME. Esse nome é necessário quando a instrução for ad hoc SQL; o nome é opcional, se for uma chamada de procedimento.  
  
 Para agregação, o consumidor transmite o parâmetro *pUnkOuter* com o controlador IUnknown.  
  
 As propriedades do objeto conjunto de linhas de parâmetro com valor de tabela são somente leitura, portanto, não se espera que o consumidor defina as propriedades em *rgPropertySets*.  
  
 Para o membro *rgPropertySets* de cada estrutura DBCOLUMNDESC, o consumidor pode especificar propriedades adicionais para cada coluna. Essas propriedades pertencem ao conjunto de propriedades DBPROPSET_SQLSERVERCOLUMN. Elas permitem que você especifique as configurações computadas e padrão de cada coluna. Elas também dão suporte a propriedades de coluna existentes, como nulidade e identidade.  
  
 Para recuperar informações correspondentes de um objeto do conjunto de linhas do parâmetro com valor de tabela, o consumidor usa IRowsetInfo::GetProperties.  
  
 Para recuperar informações sobre o status nulo, exclusivo, computado e de atualização de cada coluna, o consumidor usa IColumnsRowset:: GetColumnsRowset ou IColumnsInfo:: GetColumnInfo. Esses métodos fornecem informações detalhadas sobre cada coluna do conjunto de linhas do parâmetro com valor de tabela.  
  
 O consumidor especifica o tipo de cada coluna do parâmetro com valor de tabela. Esse procedimento é semelhante à forma de especificação de colunas quando uma tabela é criada no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O consumidor obtém um objeto de conjunto de linhas de parâmetro com valor de tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo por meio do parâmetro de saída *ppRowset* .  
  
## <a name="dynamic-scenario"></a>Cenário dinâmico  
 Quando o consumidor não tem informações de tipo, ele deve usar IOpenRowset:: OpenRowset para instanciar objetos de conjunto de linhas de parâmetro com valor de tabela. O consumidor deve fornecer ao provedor somente o nome do tipo.  
  
 Nesse cenário, o provedor obtém as informações de tipo sobre um objeto do conjunto de linhas do parâmetro com valor de tabela do servidor em nome do consumidor.  
  
 Os parâmetros *pTableID* e *pUnkOuter* devem ser definidos como no cenário estático. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo obtém as informações de tipo (restrições e informações de coluna) do servidor e retorna um objeto de conjunto de linhas de parâmetro com valor de tabela por meio do parâmetro *ppRowset* . Essa operação requer comunicação com o servidor e, portanto, não tem desempenho tão bom quanto no cenário estático. O cenário dinâmico só funciona com chamadas de procedimento com parâmetros.  
  
## <a name="see-also"></a>Consulte Também  
 [Os parâmetros com valor de tabela &#40;OLE DB&#41;](table-valued-parameters-ole-db.md)   
 [Usar parâmetros com valor de tabela &#40;OLE DB&#41;](../native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
