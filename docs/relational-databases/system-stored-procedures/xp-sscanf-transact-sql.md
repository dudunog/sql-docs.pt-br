---
description: xp_sscanf (Transact-SQL)
title: xp_sscanf (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_sscanf_TSQL
- xp_sscanf
dev_langs:
- TSQL
helpviewer_keywords:
- xp_sscanf
ms.assetid: 619a9df1-7008-407e-a75a-bc6f851454a8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d121e9a0c1540ec42ee5c9becb0facc24d49c287
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88419160"
---
# <a name="xp_sscanf-transact-sql"></a>xp_sscanf (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Lê dados da cadeia de caracteres para os locais de argumento especificados por cada argumento de formato.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_sscanf { string OUTPUT , format } [ ,argument [ ,...n ] ]   
```  
  
## <a name="arguments"></a>Argumentos  
 **cadeia de caracteres**  
 É a cadeia de caracteres a partir da qual os valores de argumentos serão lidos.  
  
 OUTPUT  
 Quando especificado, coloca o valor do *argumento* no parâmetro de saída.  
  
 *format*  
 É uma cadeia de caracteres formatada semelhante ao que é suportado pela função **sscanf** em linguagem C. Atualmente, é oferecido suporte apenas para o argumento de formato %s.  
  
 *argument*  
 É uma variável **varchar** definida como o valor do argumento de *formato* correspondente.  
  
 *n*  
 É um espaço reservado que indica que no máximo 50 argumentos podem ser especificados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **xp_sscanf** retorna a seguinte mensagem:  
  
 `Command(s) completed successfully.`  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `xp_sscanf` para extrair dois valores de uma cadeia de caracteres de origem com base em suas posições no formato da cadeia de caracteres de origem.  
  
```  
DECLARE @filename varchar (20), @message varchar (20);  
EXEC xp_sscanf 'sync -b -fproducts10.tmp -rrandom', 'sync -b -f%s -r%s',   
  @filename OUTPUT, @message OUTPUT;  
SELECT @filename, @message;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
-------------------- --------------------   
products10.tmp        random  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [&#41;&#40;Transact-SQL de xp_sprintf ](../../relational-databases/system-stored-procedures/xp-sprintf-transact-sql.md)  
  
  
