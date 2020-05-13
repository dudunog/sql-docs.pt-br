---
title: Elemento de índice (DTA)
description: No utilitário dta, o elemento Index contém informações sobre um índice que você deseja criar ou remover para uma configuração especificada pelo usuário.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Index element (DTA)
ms.assetid: 447d3964-b387-40f6-9189-71386774c29e
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: df13c50363723ca9351b6e73cf5db59bc6a183d9
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831556"
---
# <a name="index-element-dta"></a>Elemento de índice (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Contém informações sobre um índice que você quer criar ou descartar para uma configuração especificada pelo usuário.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Recommendation>  
  <Create>  
    <Index [Clustered | Unique | Online | IndexSizeInMB | NumberOfRows             | QUOTED_IDENTIFIER | ARITHABORT | CONCAT_NULL_YIELDS_NULL             | ANSI_NULLS | ANSI_PADDING | ANSI_WARNINGS  
            | NUMERIC_ROUNDABORT]  
     ...code removed here...  
    </Index>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo de índice|Tipo de dados|Descrição|  
|---------------------|---------------|-----------------|  
|**Clusterizado**|**booleano**|Opcional. Especifica um índice clusterizado. Defina como "verdadeiro" ou "falso". Por exemplo:<br /><br /> `<Index Clustered="true">`<br /><br /> Por padrão, esse atributo é definido como "falso".|  
|**Exclusivo**|**booleano**|Opcional. Especifica um índice exclusivo. Defina como "verdadeiro" ou "falso". Por exemplo:<br /><br /> `<Index Unique="true">`<br /><br /> Por padrão, esse atributo é definido como "falso".|  
|**Online**|**booleano**|Opcional. Especifica um índice que pode executar operações enquanto o servidor estiver online, que requer espaço temporário em disco. Defina como "verdadeiro" ou "falso". Por exemplo:<br /><br /> `<Index Online="true">`<br /><br /> Por padrão, esse atributo é definido como "falso".<br /><br /> Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).|  
|**IndexSizeInMB**|**double**|Opcional. Especifica o tamanho máximo do índice em megabytes, por exemplo:<br /><br /> `<Index IndexSizeInMB="873.75">`<br /><br /> Sem configuração padrão.|  
|**NumberOfRows**|**inteiro**|Opcional. Simula tamanhos de índice diferentes que efetivamente simulam tamanhos de tabela diferentes. Por exemplo:<br /><br /> `<Index NumberOfRows="3000">`<br /><br /> Sem configuração padrão.|  
|**QUOTED_IDENTIFIER**|**booleano**|Opcional. Faz com que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] siga as regras ISO relativas às aspas que delimitam identificadores e cadeias de caracteres literais. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index QUOTED_IDENTIFIER [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md).|  
|**ARITHABORT**|**booleano**|Opcional. Causa o encerramento da consulta quando ocorre estouro ou erro de divisão por zero durante a execução da consulta. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index ARITHABORT [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md).|  
|**CONCAT_NULL_YIELDS_**<br /><br /> **NULL**|**booleano**|Opcional. Controla se os resultados de concatenação serão ou não tratados como valores de cadeia de caracteres nulos ou vazios. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index CONCAT_NULL_YIELDS_NULL [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md).|  
|**ANSI_NULLS**|**booleano**|Opcional. Especifica o comportamento compatível ISO dos operadores de comparação Igual a (=) e É diferente de (<>) quando usados com valores nulos. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index ANSI_NULLS [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md).|  
|**ANSI_PADDING**|**booleano**|Opcional. Controla o modo como uma coluna armazena valores menores que o tamanho definido. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index ANSI_PADDING [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md).|  
|**ANSI_WARNINGS**|**booleano**|Opcional. Especifica o comportamento padrão ISO para várias condições de erro. Esse atributo precisará ser habilitado caso o índice esteja em coluna computada ou exibição. Por exemplo, a sintaxe a seguir define esse atributo como:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md).|  
|**NUMERIC_ROUNDABORT**|**booleano**|Opcional. Especifica o nível dos relatórios de erro gerados quando o arredondamento de uma expressão provoca perda de exatidão. Esse atributo precisará ser desabilitado caso o índice pertença a uma coluna computada ou exibição.<br /><br /> A sintaxe a seguir define esse atributo como:<br /><br /> `<Index ANSI_WARNING [...]>`<br /><br /> Por padrão, esse atributo é desabilitado.<br /><br /> Para obter mais informações, veja [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md).|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|Nenhum.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma vez para cada um dos elementos **Create** ou **Drop** se nenhuma outra estrutura física de design for especificada com os elementos **Statistics** ou **Heap** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Create &#40;DTA&#41;](../../tools/dta/create-element-dta.md)<br /><br /> Elemento**Drop** . Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.|  
|**Elementos filho**|[Elemento Name para o índice &#40;DTA&#41;](../../tools/dta/name-element-for-index-dta.md)<br /><br /> [Elemento Column para Index &#40;DTA&#41;](../../tools/dta/column-element-for-index-dta.md)<br /><br /> Elemento**PartitionScheme** . Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> Elemento**PartitionColumn** . Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> [Elemento Filegroup para o índice &#40;DTA&#41;](../../tools/dta/filegroup-element-for-index-dta.md)<br /><br /> Elemento**NumberOfReferences** . Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.<br /><br /> Elemento**PercentUsage** . Para obter mais informações, consulte o esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja a [Amostra de arquivo de entrada XML com a configuração especificada pelo usuário &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
