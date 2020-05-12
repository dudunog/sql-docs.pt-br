---
title: TEXTVALID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs:
- TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 456b429023d4a63349b8c37e5432ff7ed920debd
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832861"
---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>Funções de texto e imagem – TEXTVALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Uma função **text**, **ntext** ou **image** que verifica se um ponteiro de texto específico é válido.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] A funcionalidade alternativa não está disponível.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
TEXTVALID ( 'table.column' ,text_ ptr )  
```  
  
## <a name="arguments"></a>Argumentos  
 *table*  
 É o nome da tabela que será usada.  
  
 *column*  
 É o nome da coluna que será usada.  
  
 *text_ptr*  
 É o ponteiro de texto a ser verificado.  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 Retorna 1 se o ponteiro for válido e 0 se o ponteiro não for válido. Observe que o identificador para a coluna **text** deve incluir o nome da tabela. Não é possível usar UPDATETEXT, WRITETEXT ou READTEXT sem um ponteiro de texto válido.  
  
 As seguintes funções e instruções também são úteis quando você trabalha com os dados **text**, **ntext** e **image**.  
  
|Função ou instrução|DESCRIÇÃO|  
|---------------------------|-----------------|  
|PATINDEX **(** ' _%pattern%_ ' **,** _expression_ **)**|Retorna a posição de caractere de uma cadeia de caracteres especificada nas colunas **text** e **ntext**.|  
|DATALENGTH **(** _expression_ **)**|Retorna o comprimento dos dados nas colunas **text**, **ntext** e **image**.|  
|SET TEXTSIZE|Retorna o limite, em bytes, dos dados **text**, **ntext** ou **image** a serem retornados com uma instrução SELECT.|  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir informa se um ponteiro de texto válido existe para cada valor na coluna `logo` da tabela `pub_info`.  
  
> [!NOTE]  
>  Para executar este exemplo, é necessário instalar o banco de dados **pubs**.  
  
```  
USE pubs;  
GO  
SELECT pub_id, 'Valid (if 1) Text data'   
   = TEXTVALID ('pub_info.logo', TEXTPTR(logo))   
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id Valid (if 1) Text data   
------ ----------------------   
0736   1                        
0877   1                        
1389   1                        
1622   1                        
1756   1                        
9901   1                        
9952   1                        
9999   1                        
  
(8 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [Funções de texto e imagem &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  
