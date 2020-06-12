---
title: Desenvolvendo com XMLA no Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, data mining
- commands [XML for Analysis]
- data mining [XML for Analysis]
- XMLA, data mining
- XML for Analysis, Analysis Services tasks
- XMLA, Analysis Services tasks
ms.assetid: 54445ee7-720c-4683-99a6-e75b3dcca904
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2f5455b71306b3dd75406f107e5c1e971f6b923b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544998"
---
# <a name="developing-with-xmla-in-analysis-services"></a>Desenvolvendo com XMLA no Analysis Services
  O XMLA (XML for Analysis) é um protocolo XML baseado em SOAP, criado especificamente para acesso a dados universal para qualquer fonte de dados multidimensional padrão que pode ser acessado por meio de uma conexão HTTP. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa o XMLA como seu único protocolo para se comunicar com aplicativos cliente. Basicamente, todas as bibliotecas de cliente com suporte do Analysis Services formulam solicitações e respostas em XMLA.  
  
 Como desenvolvedor, você pode usar o XMLA para integrar um aplicativo cliente ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], sem qualquer dependência das interfaces do .NET Framework ou COM. Os requisitos de aplicativo que incluem a hospedagem em uma ampla variedade de plataformas podem ser atendidos com o uso do XMLA e de uma conexão HTTP com o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é totalmente compatível com a especificação 1.1 do XMLA, mas também a estende para habilitar o suporte para definição, manipulação e controle de dados. As extensões do Analysis Services são referidas como ASSL (Analysis Services Scripting Language). Usar XMLA e ASSL juntos habilita uma variedade maior de funcionalidades do que o XMLA fornece sozinho. Para obter mais informações sobre o ASSL, consulte [desenvolvendo com a linguagem de script Analysis Services &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Gerenciando conexões e sessões &#40;XMLA&#41;](managing-connections-and-sessions-xmla.md)|Descreve como se conectar a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e como gerenciar sessões e a capacidade de manutenção de status do processo no XMLA.|  
|[Manipulando erros e avisos &#40;&#41;XMLA](handling-errors-and-warnings-xmla.md)|Descreve como o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] retorna informações de erro e de aviso para métodos e comandos no XMLA.|  
|[Definindo e identificando objetos &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects)|Descreve identificadores de objetos e referências de objeto, e como usar identificadores e referências em comandos XMLA.|  
|[Gerenciando transações &#40;&#41;XMLA](managing-transactions-xmla.md)|Fornece detalhes sobre como usar os comandos [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla), [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)e [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) para definir e gerenciar explicitamente uma transação na sessão XMLA atual.|  
|[Cancelando comandos &#40;XMLA&#41;](../multidimensional-models-scripting-language-assl-xmla/canceling-commands-xmla.md)|Descreve como usar o comando [Cancel](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/cancel-element-xmla)para cancelar comandos, sessões e conexões no XMLA.|  
|[Executando operações em lote &#40;XMLA&#41;](performing-batch-operations-xmla.md)|Descreve como usar o comando [batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) para executar vários comandos XMLA, em série ou em paralelo, na mesma transação ou como transações separadas, usando um único método de [execução](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) XMLA.|  
|[Criando e alterando objetos &#40;XMLA&#41;](creating-and-altering-objects-xmla.md)|Descreve como usar os comandos [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla), [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla)e [delete](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) , juntamente com os elementos ASSL (linguagem de script do Analysis Services), para definir, alterar ou remover objetos de uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância do.|  
|[Bloqueando e desbloqueando bancos de dados &#40;XMLA&#41;](locking-and-unlocking-databases-xmla.md)|Detalhes de como usar os comandos [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) e [Unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) para bloquear e desbloquear um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados.|  
|[Processando objetos &#40;XMLA&#41;](processing-objects-xmla.md)|Descreve como usar o comando [process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) para processar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objeto.|  
|[Mesclando partições &#40;&#41;XMLA](merging-partitions-xmla.md)|Descreve como usar o comando [MergePartitions](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/mergepartitions-element-xmla) para mesclar partições em uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] instância do.|  
|[Criando agregações &#40;XMLA&#41;](designing-aggregations-xmla.md)|Descreve como usar o comando [DesignAggregations](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/designaggregations-element-xmla) , no modo iterativo ou em lotes, para criar agregações para um design de agregação no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Fazendo backup, restaurando e sincronizando bancos de dados &#40;XMLA&#41;](backing-up-restoring-and-synchronizing-databases-xmla.md)|Descreve como usar os comandos [backup](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/backup-element-xmla) e [Restore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/restore-element-xmla) para fazer backup e restaurar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados de um arquivo de backup.<br /><br /> Também descreve como usar o comando [Synchronize](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/synchronize-element-xmla) para sincronizar um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] banco de dados com um banco de dados existente na mesma instância ou em uma instância diferente.|  
|[Inserindo, atualizando e descartando Membros &#40;XMLA&#41;](inserting-updating-and-dropping-members-xmla.md)|Descreve como usar os comandos [Insert](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [Update](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)e [drop](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) para adicionar, alterar ou excluir membros de uma dimensão habilitada para gravação.|  
|[Atualizando células &#40;&#41;XMLA](updating-cells-xmla.md)|Descreve como usar o comando [UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla) para alterar os valores de células em uma partição habilitada para gravação.|  
|[Gerenciando caches &#40;XMLA&#41;](managing-caches-xmla.md)|Detalhes de como usar o comando [ClearCache](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/clearcache-element-xmla) para limpar os caches de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] objetos.|  
|[Monitoramento de rastreamentos &#40;&#41;XMLA](monitoring-traces-xmla.md)|Descreve como usar o comando [Subscribe](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/subscribe-element-xmla) para assinar e monitorar um rastreamento existente em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
  
## <a name="data-mining-with-xmla"></a>Mineração de dados com o XMLA  
 O XML for Analysis dá suporte completo a conjuntos de linhas do esquema de mineração de dados. Esses conjuntos de linhas fornecem informações para consultar modelos de Data Mining usando o método [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) . Para obter mais informações sobre conjuntos de linhas de esquema Data Mining, consulte conjuntos de linhas de [esquema de mineração de dados](https://docs.microsoft.com/bi-reference/schema-rowsets/data-mining/data-mining-schema-rowsets) 
  
 Para obter mais informações sobre DMX, consulte [Data Mining Extensions &#40;DMX&#41; referência](/sql/dmx/data-mining-extensions-dmx-reference).  
  
## <a name="namespace-and-schema"></a>Namespace e esquema  
  
### <a name="namespace"></a>Namespace  
 O esquema definido nesta especificação usa o namespace XML `https://schemas.microsoft.com/AnalysisServices/2003/Engine` e a abreviação padrão "DDL".  
  
### <a name="schema"></a>Esquema  
 A definição de um esquema da linguagem XSD para a linguagem de definição do objeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] baseia-se na definição dos elementos de esquema e na hierarquia desta seção.  
  
## <a name="extensibility"></a>Extensibilidade  
 A extensibilidade do esquema da linguagem de definição do objeto é fornecida por meio de um elemento do `Annotation` incluído em todos os objetos. Este elemento pode conter qualquer XML válido de qualquer namespace XML (diferente do namespace de destino que define o DDL), e está sujeito às seguintes regras:  
  
-   O XML pode conter somente elementos.  
  
-   Cada elemento deve ter um nome exclusivo. É recomendado que o valor de `Name` faça referência ao namespace de destino.  
  
 Estas regras são impostas para que o conteúdo da marca `Annotation` seja exposto como um conjunto de pares Nome/Valor por meio do DSO 9.0 (Decision Support Objects).  
  
 Os comentários e o espaço em branco na marca `Annotation` que não forem incluídos com um elemento filho podem não ser preservados. Além disso, todos os elementos devem ser de leitura/gravação; elementos somente leitura são ignorados.  
  
 O esquema de linguagem de definição do objeto é fechado, sendo que o servidor não permite a substituição de tipos derivados para elementos definidos no esquema. Dessa forma, o servidor só aceitará o conjunto de elementos definido aqui e nenhum outro elemento ou atributo. Elementos desconhecidos farão com que o mecanismo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gere um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo com a linguagem de script Analysis Services &#40;ASSL&#41;](../multidimensional-models/scripting-language-assl/developing-with-analysis-services-scripting-language-assl.md)   
 [Entendendo a arquitetura Microsoft OLAP](../multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)  
  
  
