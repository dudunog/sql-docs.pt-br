---
description: '&#x40;&#x40;Versão – funções de configuração do Transact-SQL'
title: '@@VERSION (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/20/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@VERSION'
- '@@VERSION_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@VERSION function'
- current SQL Server installation information
- versions [SQL Server], @@VERSION
- processors [SQL Server], types
ms.assetid: 385ba80e-7c28-41a5-9cdb-5648f3785983
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7670a4e4cdb412ad55bfef01f8322c37023335e2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97422042"
---
# <a name="x40x40version---transact-sql-configuration-functions"></a>&#x40;&#x40;Versão – funções de configuração do Transact-SQL
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna informações de compilação e sistema para a instalação atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
@@VERSION  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **nvarchar**  
  
## <a name="remarks"></a>Comentários  
 Os resultados de @@VERSION são apresentados como uma cadeia de caracteres nvarchar. Use a função [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md) para recuperar os valores de propriedade individuais.  
  
 Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as informações a seguir são retornadas.  
  
-   Versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Arquitetura do processador  
  
-   Data de compilação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Instrução de direitos autorais  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edição  
  
-   Versão do sistema operacional  
  
 Para o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], as informações a seguir são retornadas.  
  
-   Edição- "Microsoft SQL Azure"  
  
-   Nível do produto- "(RTM)"  
  
-   Versão do produto  
  
-   Data de compilação  
  
-   Instrução de direitos autorais  

> [!NOTE]  
> Estamos cientes de um problema em que a versão de produto relatada por @@VERSION está incorreta para o Banco de Dados SQL do Azure. A versão do mecanismo de banco de dados do SQL Server executada pelo Banco de Dados SQL do Azure sempre está à frente da versão local do SQL Server e inclui as correções de segurança mais recentes. Isso significa que o nível de patch está sempre pareado com a versão local do SQL Server ou à frente dela e que os recursos mais recentes disponíveis no SQL Server estão disponíveis no Banco de Dados SQL do Azure.
>
> Para determinar programaticamente a edição do mecanismo, use SELECT SERVERPROPERTY('EngineEdition'). Esta consulta retornará '5' para o Banco de Dados SQL do Azure e '8' para a Instância Gerenciada de SQL do Azure.
>
> A documentação será atualizada depois que esse problema for resolvido.

  
## <a name="examples"></a>Exemplos  
  
### <a name="a-return-the-current-version-of-ssnoversion"></a>A: Retornar a versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 O exemplo a seguir mostra o retorno das informações de versão da instalação atual.  
  
```sql
SELECT @@VERSION AS 'SQL Server Version';  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-return-the-current-version-of-ssdw"></a>B. Retornar a versão atual do [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
  
```sql
SELECT @@VERSION AS 'SQL Server PDW Version';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [SERVERPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/serverproperty-transact-sql.md)  
  
  

