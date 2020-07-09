---
title: SUSER_SNAME (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SUSER_SNAME_TSQL
- SUSER_SNAME
dev_langs:
- TSQL
helpviewer_keywords:
- security identification names [SQL Server]
- logins [SQL Server], users
- SIDs [SQL Server]
- SUSER_SNAME function
- users [SQL Server], logins
- logins [SQL Server], names
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- names [SQL Server], logins
ms.assetid: 11ec7d86-d429-4004-a436-da25df9f8761
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 29a0fc66901fe358113f244a770e70a9dbe2e12b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85994002"
---
# <a name="suser_sname-transact-sql"></a>SUSER_SNAME (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna o nome de logon associado a um número de identificação de segurança (SID).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SUSER_SNAME ( [ server_user_sid ] )   
```  
  
## <a name="arguments"></a>Argumentos  
 *server_user_sid*  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
 É o número opcional de identificação de segurança do logon. *server_user_sid* é **varbinary(85)** . *server_user_sid* pode ser o número de identificação de segurança de qualquer logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ou usuário ou grupo do Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Se o *server_user_sid* não for especificado, serão retornadas informações sobre o usuário atual. Se o parâmetro contiver a palavra NULL, retornará NULL.  
  
## <a name="return-types"></a>Tipos de retorno  
 **nvarchar(128)**  
  
## <a name="remarks"></a>Comentários  
 SUSER_SNAME pode ser usado como uma restrição DEFAULT em ALTER TABLE ou CREATE TABLE. SUSER_SNAME pode ser usado em uma lista de seleção, em uma cláusula WHERE e em qualquer lugar em que uma expressão for permitida. SUSER_SNAME sempre deve ser seguido de parênteses, ainda que nenhum parâmetro seja especificado.  
  
 Quando chamado sem um argumento, SUSER_SNAME retorna o nome do contexto de segurança atual. Quando chamado sem um argumento em um lote que alternou o contexto usando EXECUTE AS, SUSER_SNAME retorna o nome do contexto representado. Quando chamado de um contexto representado, ORIGINAL_LOGIN retorna o nome do contexto original.  
  
## <a name="sssdsfull-remarks"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] Comentários  
 SUSER_NAME sempre retorna o nome de logon para o contexto de segurança atual.  
  
 A instrução SUSER_SNAME não oferece suporte à execução usando um contexto de segurança representado por meio de EXECUTE AS.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-suser_sname"></a>a. Usando SUSER_SNAME  
 O exemplo a seguir retorna o nome de logon para o contexto de segurança atual.  
  
```  
SELECT SUSER_SNAME();  
GO  
```  
  
### <a name="b-using-suser_sname-with-a-windows-user-security-id"></a>B. Usando SUSER_SNAME com um identificador de segurança de usuário do Windows  
 O exemplo seguinte retorna o nome de logon associado a um número de identificação de segurança do Windows.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
```  
SELECT SUSER_SNAME(0x010500000000000515000000a065cf7e784b9b5fe77c87705a2e0000);  
GO  
```  
  
### <a name="c-using-suser_sname-as-a-default-constraint"></a>C. Usando SUSER_SNAME como uma restrição DEFAULT  
 O exemplo a seguir usa `SUSER_SNAME` como uma restrição `DEFAULT` em uma instrução `CREATE TABLE`.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sname_example  
(  
login_sname sysname DEFAULT SUSER_SNAME(),  
employee_id uniqueidentifier DEFAULT NEWID(),  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sname_example DEFAULT VALUES;  
GO  
```  
  
### <a name="d-calling-suser_sname-in-combination-with-execute-as"></a>D. Chamando SUSER_SNAME em combinação com EXECUTE AS  
 Este exemplo mostra o comportamento de SUSER_SNAME quando chamado de um contexto representado.  
  
**Aplica-se a**: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior
  
```  
SELECT SUSER_SNAME();  
GO  
EXECUTE AS LOGIN = 'WanidaBenShoof';  
SELECT SUSER_SNAME();  
REVERT;  
GO  
SELECT SUSER_SNAME();  
GO  
  
```  
  
 Este é o conjunto de resultados.  
  
 ```
sa  
WanidaBenShoof  
sa
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-suser_sname"></a>E. Usando SUSER_SNAME  
 O exemplo seguinte retorna o nome de logon do número de identificação de segurança com um valor de `0x01`.  
  
```  
SELECT SUSER_SNAME(0x01);  
GO  
```  
  
### <a name="f-returning-the-current-login"></a>F. Retornando o logon atual  
 O exemplo a seguir retorna o nome de logon do logon atual.  
  
```  
SELECT SUSER_SNAME() AS CurrentLogin;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SUSER_SID &#40;Transact-SQL&#41;](../../t-sql/functions/suser-sid-transact-sql.md)   
 [Entidades &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.server_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md)  
  
  

