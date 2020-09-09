---
description: sp_OAMethod (Transact-SQL)
title: sp_OAMethod (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_OAMethod
- sp_OAMethod_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_OAMethod
ms.assetid: 1dfaebe2-c7cf-4041-a586-5d04faf2e25e
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 7442e3af4bf0233e51f32d7c8e6f034d69598046
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89526559"
---
# <a name="sp_oamethod-transact-sql"></a>sp_OAMethod (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Chama um método de um objeto OLE.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_OAMethod objecttoken , methodname  
    [ , returnvalue OUTPUT ]   
    [ , [ @parametername = ] parameter [ OUTPUT ] [ ...n ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *objecttoken*  
 É o token do objeto de um objeto OLE criado anteriormente usando **sp_OACreate**.  
  
 *MethodName*  
 É o nome de método do objeto OLE a ser chamado.  
  
 _returnvalue_**saída** de ReturnValue    
 É o valor de retorno do método do objeto OLE. Se for especificado, deverá ser uma variável local do tipo de dados apropriado.  
  
 Se o método retornar um único valor, especifique uma variável local para *ReturnValue*, que retorna o valor de retorno do método na variável local ou não especifica *ReturnValue*, que retorna o valor de retorno do método para o cliente como um conjunto de resultados de uma única coluna e de linha única.  
  
 Se o valor de retorno do método for um objeto OLE, *ReturnValue* deverá ser uma variável local do tipo de dados **int**. Um token de objeto é armazenado na variável local e esse token de objeto pode ser usado com outros procedimentos armazenados de automação OLE.  
  
 Quando o valor de retorno do método for uma matriz, se *ReturnValue* for especificado, ele será definido como NULL.  
  
 Um erro será gerado quando qualquer um dos seguintes ocorrer:  
  
-   *ReturnValue* é especificado, mas o método não retorna um valor.  
  
-   O método retornar uma matriz com mais de duas dimensões.  
  
-   O método retornar uma matriz como um parâmetro de saída.  
  
`[ _@parametername = ] parameter[ OUTPUT ]` É um parâmetro de método. Se especificado, o *parâmetro* deve ser um valor do tipo de dados apropriado.  
  
 Para obter o valor de retorno de um parâmetro de saída, o *parâmetro* deve ser uma variável local do tipo de dados apropriado e a **saída** deve ser especificada. Se um parâmetro constante for especificado ou se a **saída** não for especificada, qualquer valor de retorno de um parâmetro de saída será ignorado.  
  
 Se especificado, *ParameterName* deve ser o nome do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] parâmetro nomeado. Observe que **@** não _parametername_is uma [!INCLUDE[tsql](../../includes/tsql-md.md)] variável local. O sinal de arroba ( **@** ) é removido e *ParameterName*é passado para o objeto OLE como o nome do parâmetro. Todos os parâmetros nomeados deverão ser especificados depois que todos os parâmetros posicionais forem especificados.  
  
 *n*  
 É um espaço reservado que indica que vários parâmetros podem ser especificados.  
  
> [!NOTE]
>  * \@ ParameterName* pode ser um parâmetro nomeado porque faz parte do método especificado e é passado para o objeto. Os outros parâmetros deste procedimento armazenado são especificados por posição, não por nome.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou um número diferente de zero (falha) que é o valor inteiro do HRESULT retornado pelo objeto de Automação OLE.  
  
 Para obter mais informações sobre códigos de retorno HRESULT, [códigos de retorno de automação OLE e informações de erro](../../relational-databases/stored-procedures/ole-automation-return-codes-and-error-information.md).  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Se o valor de retorno do método for uma matriz com uma ou duas dimensões, a matriz será retornada ao cliente como um conjunto de resultados:  
  
-   Uma matriz unidimensional é retornada ao cliente como um conjunto de resultados de uma linha, com tantas colunas quanto houver elementos na matriz. Em outras palavras, a matriz é retornada como (colunas).  
  
-   Uma matriz bidimensional é retornada ao cliente como um conjunto de resultados com tantas colunas quanto houver elementos na primeira dimensão da matriz e com tantas linhas quanto houver elementos na segunda dimensão da matriz. Em outras palavras, a matriz é retornada como (colunas, linhas).  
  
 Quando um valor de retorno de propriedade ou um valor de retorno de método é uma matriz, **sp_OAGetProperty** ou **sp_OAMethod** retorna um conjunto de resultados para o cliente. (Os parâmetros de saída de método não podem ser matrizes.) Esses procedimentos examinam todos os valores de dados na matriz para determinar os tipos de dados apropriados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os tamanhos dos dados a serem usados para cada coluna no conjunto de resultados. Para uma coluna específica, esses procedimentos usam o tipo de dados e o tamanho necessários para representar todos os valores de dados nesta coluna.  
  
 Quando todos os valores de dados em uma coluna compartilharem o mesmo tipo de dados, esse tipo de dados será usado para a coluna inteira. Quando os valores de dados em uma coluna forem de tipos de dados diferentes, o tipo de dados da coluna inteira será escolhido com base no quadro a seguir.  
  
||INT|FLOAT|money|DATETIME|varchar|NVARCHAR|  
|------|---------|-----------|-----------|--------------|-------------|--------------|  
|**int**|**int**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**float**|**float**|**float**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**money**|**money**|**money**|**money**|**varchar**|**varchar**|**nvarchar**|  
|**datetime**|**varchar**|**varchar**|**varchar**|**datetime**|**varchar**|**nvarchar**|  
|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**varchar**|**nvarchar**|  
|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|**nvarchar**|  
  
## <a name="remarks"></a>Comentários  
 Você também pode usar **sp_OAMethod** para obter um valor de propriedade.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de servidor fixa **sysadmin** ou a permissão execute diretamente neste procedimento armazenado. `Ole Automation Procedures` a configuração deve ser **habilitada** para usar qualquer procedimento do sistema relacionado à automação OLE.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calling-a-method"></a>a. Chamando um método  
 O exemplo a seguir chama o `Connect` método do objeto **SqlServer** criado anteriormente.  
  
```  
EXEC @hr = sp_OAMethod @object, 'Connect', NULL, 'my_server',  
    'my_login', 'my_password';  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
```  
  
### <a name="b-getting-a-property"></a>B. Obtendo uma propriedade  
 O exemplo a seguir obtém a `HostName` Propriedade (do objeto **SqlServer** criado anteriormente) e a armazena em uma variável local.  
  
```  
DECLARE @property varchar(255);  
EXEC @hr = sp_OAMethod @object, 'HostName', @property OUT;  
IF @hr <> 0  
BEGIN  
   EXEC sp_OAGetErrorInfo @object  
    RETURN  
END;  
PRINT @property;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de automação OLE &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)   
 [Script de exemplo de automação OLE](../../relational-databases/stored-procedures/ole-automation-sample-script.md)  
  
  
