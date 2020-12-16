---
description: COMMIT TRANSACTION (Transact-SQL)
title: COMMIT TRANSACTION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- COMMIT
- COMMIT TRANSACTION
- COMMIT_TSQL
- COMMIT_TRANSACTION_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ending transactions [SQL Server]
- user-defined transactions [SQL Server]
- committed transactions
- transactions [SQL Server], ending
- marking end of transactions [SQL Server]
- implicit transactions
- distributed transactions [SQL Server], committed
- transactions [SQL Server], committed
- COMMIT TRANSACTION statement
- rolling back transactions, COMMIT TRANSACTION
ms.assetid: f8fe26a9-7911-497e-b348-4e69c7435dc1
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 431808195f55f2cc7d04621fcdc9ac63ab4a2a1d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474187"
---
# <a name="commit-transaction-transact-sql"></a>COMMIT TRANSACTION (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Marca o término de uma transação implícita ou explícita bem-sucedida. Se @@TRANCOUNT for 1, COMMIT TRANSACTION fará com que todas as modificações de dados desde o início da transação sejam uma parte permanente do banco de dados, liberará os recursos da transação e decrementará @@TRANCOUNT para 0. Quando @@TRANCOUNT for maior que 1, COMMIT TRANSACTION decrementará @@TRANCOUNT somente em 1 e a transação permanecerá ativa.  
  
 ![Ícone de link do artigo](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do artigo") [Convenções de sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
-- Applies to SQL Server (starting with 2008) and Azure SQL Database
  
COMMIT [ { TRAN | TRANSACTION }  [ transaction_name | @tran_name_variable ] ] [ WITH ( DELAYED_DURABILITY = { OFF | ON } ) ]  
[ ; ]  
```  
 
```syntaxsql
-- Applies to Azure Synapse Analytics and Parallel Data Warehouse Database
  
COMMIT [ TRAN | TRANSACTION ] 
[ ; ]  
``` 
 
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *transaction_name*  
 **APLICA-SE A:** SQL Server e Banco de Dados SQL do Azure
 
 É ignorado pelo [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]. *transaction_name* especifica um nome de transação atribuído por um BEGIN TRANSACTION anterior. *transaction_name* precisa estar em conformidade com as regras para identificadores, mas não pode exceder 32 caracteres. *transaction_name* indica aos programadores a qual BEGIN TRANSACTION aninhada COMMIT TRANSACTION está associada.  
  
 *\@tran_name_variable*  
 **APLICA-SE A:** SQL Server e Banco de Dados SQL do Azure  
 
É o nome de uma variável definida pelo usuário que contém um nome de transação válido. A variável precisa ser declarada com o tipo de dados char, varchar, nchar ou nvarchar. Se mais de 32 caracteres forem transmitidos à variável, apenas 32 caracteres serão usados; os demais serão truncados.  
  
 DELAYED_DURABILITY  
 **APLICA-SE A:** SQL Server e Banco de Dados SQL do Azure   

 Opção que solicita que esta transação seja confirmada com durabilidade atrasada. A solicitação será ignorada se o banco de dados for alterado com `DELAYED_DURABILITY = DISABLED` ou `DELAYED_DURABILITY = FORCED`. Para obter mais informações, veja [Controlar a durabilidade da transação](../../relational-databases/logs/control-transaction-durability.md).  
  
## <a name="remarks"></a>Comentários  
 É responsabilidade do programador do [!INCLUDE[tsql](../../includes/tsql-md.md)] emitir COMMIT TRANSACTION apenas no ponto em que todos os dados referidos pela transação estiverem logicamente corretos.  
  
 Se a transação confirmada for uma transação distribuída de [!INCLUDE[tsql](../../includes/tsql-md.md)], COMMIT TRANSACTION irá disparar MS DTC para usar um protocolo 2PC para confirmar todos os servidores envolvidos na transação. Quando uma transação local atingir dois ou mais bancos de dados na mesma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], essa instância usará um protocolo 2PC interno para confirmar todos os bancos de dados envolvidos na transação.  
  
 Quando usadas em transações aninhadas, as confirmações das transações internas não liberam recursos, nem lhes fazem modificações permanentes. As modificações de dados se tornam permanentes, com liberação dos recursos, apenas quando a transação externa é confirmada. Cada COMMIT TRANSACTION emitida quando @@TRANCOUNT é maior que um simplesmente decrementa @@TRANCOUNT em 1. Quando @@TRANCOUNT é, finalmente, decrementado para 0, toda a transação externa é confirmada. Como *transaction_name* é ignorado pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)], emitir um COMMIT TRANSACTION referenciando o nome de uma transação externa quando há transações internas pendentes apenas decrementa @@TRANCOUNT em 1.  
  
 Emitir uma COMMIT TRANSACTION quando @@TRANCOUNT é zero resulta em erro. Não há um BEGIN TRANSACTION correspondente.  
  
 Não é possível reverter uma transação após a emissão de uma instrução COMMIT TRANSACTION, porque as modificações de dados se tornam parte permanente do banco de dados.  
  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] incrementa a contagem de transações em uma instrução apenas quando essa contagem é 0 no início da instrução.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-committing-a-transaction"></a>a. Confirmando uma transação  
**APLICA-SE A:** SQL Server, Banco de Dados SQL do Azure, [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]   

O exemplo a seguir exclui um candidato a emprego. Ele usa o AdventureWorks. 
  
```sql   
BEGIN TRANSACTION;   
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;   
COMMIT TRANSACTION;   
```  
  
### <a name="b-committing-a-nested-transaction"></a>B. Confirmando uma transação aninhada  
**APLICA-SE A:** SQL Server e Banco de Dados SQL do Azure    

O exemplo a seguir cria uma tabela, gera três níveis de transações aninhadas e, em seguida, confirma a transação aninhada. Embora cada instrução `COMMIT TRANSACTION` tenha um parâmetro *transaction_name*, não há nenhuma relação entre as instruções `COMMIT TRANSACTION` e `BEGIN TRANSACTION`. Os parâmetros *transaction_name* ajudam o programador a assegurar que o número correto de confirmações seja codificado para decrementar `@@TRANCOUNT` para 0 e, assim, confirmar a transação externa. 
  
```sql   
IF OBJECT_ID(N'TestTran',N'U') IS NOT NULL  
    DROP TABLE TestTran;  
GO  
CREATE TABLE TestTran (Cola INT PRIMARY KEY, Colb CHAR(3));  
GO  
-- This statement sets @@TRANCOUNT to 1.  
BEGIN TRANSACTION OuterTran;  
  
PRINT N'Transaction count after BEGIN OuterTran = '  
    + CAST(@@TRANCOUNT AS NVARCHAR(10));  
 
INSERT INTO TestTran VALUES (1, 'aaa');  
 
-- This statement sets @@TRANCOUNT to 2.  
BEGIN TRANSACTION Inner1;  
 
PRINT N'Transaction count after BEGIN Inner1 = '  
    + CAST(@@TRANCOUNT AS NVARCHAR(10));  
  
INSERT INTO TestTran VALUES (2, 'bbb');  
  
-- This statement sets @@TRANCOUNT to 3.  
BEGIN TRANSACTION Inner2;  
  
PRINT N'Transaction count after BEGIN Inner2 = '  
    + CAST(@@TRANCOUNT AS NVARCHAR(10));  
  
INSERT INTO TestTran VALUES (3, 'ccc');  
  
-- This statement decrements @@TRANCOUNT to 2.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner2;  
 
PRINT N'Transaction count after COMMIT Inner2 = '  
    + CAST(@@TRANCOUNT AS NVARCHAR(10));  
 
-- This statement decrements @@TRANCOUNT to 1.  
-- Nothing is committed.  
COMMIT TRANSACTION Inner1;  
 
PRINT N'Transaction count after COMMIT Inner1 = '  
    + CAST(@@TRANCOUNT AS NVARCHAR(10));  
  
-- This statement decrements @@TRANCOUNT to 0 and  
-- commits outer transaction OuterTran.  
COMMIT TRANSACTION OuterTran;  
  
PRINT N'Transaction count after COMMIT OuterTran = '  
    + CAST(@@TRANCOUNT AS NVARCHAR(10));  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BEGIN DISTRIBUTED TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-distributed-transaction-transact-sql.md)   
 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)   
 [COMMIT WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/commit-work-transact-sql.md)   
 [ROLLBACK TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-transaction-transact-sql.md)   
 [ROLLBACK WORK &#40;Transact-SQL&#41;](../../t-sql/language-elements/rollback-work-transact-sql.md)   
 [SAVE TRANSACTION &#40;Transact-SQL&#41;](../../t-sql/language-elements/save-transaction-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
