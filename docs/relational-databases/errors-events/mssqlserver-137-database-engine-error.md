---
title: MSSQLSERVER_137 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 137 (Database Engine error)
ms.assetid: 47fb4212-2165-4fec-bc41-6d548465d7be
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4e780d6afaddc5ac3af0e87e6b629fb39c987879
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72305032"
---
# <a name="mssqlserver_137"></a>MSSQLSERVER_137
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|137|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|P_SCALAR_VAR_NOTFOUND|  
|Texto da mensagem|É necessário declarar a variável escalar "%.*ls".|  
  
## <a name="explanation"></a>Explicação  
Esse erro ocorre quando uma variável é usada em um script SQL sem primeiro declarar a variável. O exemplo a seguir retorna o erro 137 para as instruções SET e SELECT porque **\@mycol** não é declarada.  
  
SET @mycol = 'ContactName';  
  
SELECT @mycol;  
  
Uma das causas mais complexas desse erro inclui o uso de uma variável que é declarada fora da instrução EXECUTE. Por exemplo, a variável **\@mycol** especificada na instrução SELECT é local na instrução SELECT, por isso está fora da instrução EXECUTE.  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20);  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT @mycol FROM Production.Product;');  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se alguma das variáveis usadas em um script SQL foi declarada antes de ser usada em outro lugar no script.  
  
Reescreva o script de modo que ele não faça referência a variáveis na instrução EXECUTE que estejam declaradas fora dela. Por exemplo:  
  
USE AdventureWorks2012;  
  
GO  
  
DECLARE @mycol nvarchar(20) ;  
  
SET @mycol = 'Name';  
  
EXECUTE ('SELECT ' + @mycol + ' FROM Production.Product';) ;  
  
## <a name="see-also"></a>Consulte Também  
[EXECUTE &#40;Transact-SQL&#41;](~/t-sql/language-elements/execute-transact-sql.md)  
[Instruções SET &#40;Transact-SQL&#41;](~/t-sql/statements/set-statements-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](~/t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
