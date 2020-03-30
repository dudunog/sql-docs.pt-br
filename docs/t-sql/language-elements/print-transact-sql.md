---
title: PRINT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PRINT_TSQL
- PRINT
dev_langs:
- TSQL
helpviewer_keywords:
- PRINT statement
- user-defined messages [SQL Server]
- messages [SQL Server], PRINT statement
- displaying user-defined messages
- viewing user-defined messages
- conditionally returning messages [SQL Server]
ms.assetid: 32ba0729-c4b5-4cfb-a5aa-e8b9402be028
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cc83aca49b6147835353538d809be121756ecda6
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68072397"
---
# <a name="print-transact-sql"></a>PRINT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna uma mensagem definida pelo usuário ao cliente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
PRINT msg_str | @local_variable | string_expr  
```  
  
## <a name="arguments"></a>Argumentos  
 *msg_str*  
 É uma cadeia de caracteres ou uma constante de cadeia de caracteres Unicode. Para obter mais informações, consulte [Constantes &#40;Transact-SQL&#41;](../../t-sql/data-types/constants-transact-sql.md).  
  
 **@** *local_variable*  
 É uma variável de qualquer tipo de dados de caractere válido. **@** _local\_variable_ deve ser **char**, **nchar**, **varchar** ou **nvarchar** ou deve poder ser convertido implicitamente nesses tipos de dados.  
  
 *string_expr*  
 É uma expressão que retorna uma cadeia de caracteres. Pode incluir valores literais, funções e variáveis concatenadas. Para obter mais informações, veja [Expressões &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## <a name="remarks"></a>Comentários  
 Uma cadeia de caracteres de mensagem pode ter até 8.000 caracteres se for uma cadeia de caracteres não Unicode e 4.000 caracteres se for uma cadeia de caracteres Unicode. Cadeias de caracteres mais longas são truncadas. Os tipos de dados **varchar(max)** e **nvarchar(max)** são truncados para tipos de dados que não são maiores que **varchar(8000)** e **nvarchar(4000)** .  
  
 RAISERROR também pode ser usado para retornar mensagens. RAISERROR tem estas vantagens sobre PRINT:  
  
-   RAISERROR oferece suporte à substituição de argumentos em uma cadeia de caracteres de mensagem de erro usando um mecanismo modelado sobre a função printf da biblioteca padrão da linguagem C.  
  
-   RAISERROR pode especificar um número de erro exclusivo, uma severidade e um código de estado, além da mensagem de texto.  
  
-   RAISERROR pode ser usado para retornar mensagens definidas pelo usuário criadas com o uso do procedimento armazenado do sistema sp_addmessage.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-conditionally-executing-print-if-exists"></a>a. Executando print condicionalmente (IF EXISTS)  
 O exemplo a seguir usa a instrução `PRINT` para retornar uma mensagem condicionalmente.  
  
```  
IF @@OPTIONS & 512 <> 0  
    PRINT N'This user has SET NOCOUNT turned ON.';  
ELSE  
    PRINT N'This user has SET NOCOUNT turned OFF.';  
GO  
```  
  
### <a name="b-building-and-displaying-a-string"></a>B. Construindo e exibindo uma cadeia de caracteres  
 O exemplo a seguir converte os resultados da função `GETDATE` em um tipo de dados `nvarchar` e o concatena com o texto literal a ser retornado por `PRINT`.  
  
```  
-- Build the message text by concatenating  
-- strings and expressions.  
PRINT N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
GO  
-- This example shows building the message text  
-- in a variable and then passing it to PRINT.  
-- This was required in SQL Server 7.0 or earlier.  
DECLARE @PrintMessage nvarchar(50);  
SET @PrintMessage = N'This message was printed on '  
    + RTRIM(CAST(GETDATE() AS nvarchar(30)))  
    + N'.';  
PRINT @PrintMessage;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-conditionally-executing-print"></a>C. Executando print condicionalmente  
 O exemplo a seguir usa a instrução `PRINT` para retornar uma mensagem condicionalmente.  
  
```  
IF DB_ID() = 1  
    PRINT N'The current database is master.';  
ELSE  
    PRINT N'The current database is not master.';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)   
 [RAISERROR &#40;Transact-SQL&#41;](../../t-sql/language-elements/raiserror-transact-sql.md)  
  
  

