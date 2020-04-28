---
title: Comando DROP TABLE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- drop table command [ODBC]
ms.assetid: bc50459b-8861-4889-84a9-129ae9065aa8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 779c519f720027aea3a6f6cf2587d3c6e0b59b52
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303417"
---
# <a name="drop-table-command"></a>Comando DROP TABLE
Remove uma tabela do banco de dados especificado com a fonte e a exclui do disco.  
  
 O driver ODBC do Visual FoxPro dá suporte à sintaxe de linguagem nativa do Visual FoxPro para este comando. Para obter informações específicas do driver, consulte os comentários.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DROP TABLE TableName | FileName | ?  
```  
  
## <a name="settings"></a>Configurações  
 *TableName*  
 Especifica a tabela a ser removida do banco de dados especificado com a fonte e para excluir do disco.  
  
 *FileName*  
 Especifica uma tabela gratuita a ser excluída do disco.  
  
 ?  
 Exibe a caixa de diálogo remover da qual é possível escolher uma tabela a ser removida do banco de dados especificado com a fonte e excluir do disco.  
  
## <a name="remarks"></a>Comentários  
 Quando DROP TABLE é emitido, todos os índices primários, valores padrão e regras de validação associados à tabela também são removidos. A descartar tabela também afetará outras tabelas no banco de dados especificado com a origem se essas tabelas tiverem regras ou relações associadas à tabela que está sendo removida. As regras e as relações não são mais válidas quando a tabela é removida do banco de dados.  
  
## <a name="driver-remarks"></a>Comentários do driver  
 Quando o aplicativo envia a instrução SQL do ODBC, solte a tabela para a fonte de dados, o driver ODBC do Visual FoxPro converte o comando no comando da tabela FoxProDROP do Visual usando a sintaxe mostrada na tabela a seguir.  
  
|Sintaxe ODBC|Fonte de dados|Sintaxe do Visual FoxPro|  
|-----------------|-----------------|--------------------------|  
|REMOVER tabela *base – nome da tabela*|Banco de dados (arquivo. DBC)|REMOVER tabela *TableName* excluir|  
||Diretório de tabelas livres (arquivos. dbf)|APAGAR *dbfName*<br /><br /> APAGAR *cdxName*<br /><br /> APAGAR *fptName*|
