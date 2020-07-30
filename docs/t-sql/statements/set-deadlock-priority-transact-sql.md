---
title: SET DEADLOCK_PRIORITY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET DEADLOCK_PRIORITY
- DEADLOCK_PRIORITY_TSQL
- SET_DEADLOCK_PRIORITY_TSQL
- DEADLOCK_PRIORITY
dev_langs:
- TSQL
helpviewer_keywords:
- deadlocks [SQL Server], priority settings
- DEADLOCK_PRIORITY option
- locking [SQL Server], deadlocks
- priority deadlock settings [SQL Server]
- SET DEADLOCK_PRIORITY statement
ms.assetid: 810a3a8e-3da3-4bf9-bb15-7b069685a1b6
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3786cdf92fce5c983e86b8f825d9d57a24e92dc3
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394125"
---
# <a name="set-deadlock_priority-transact-sql"></a>SET DEADLOCK_PRIORITY (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Especifica a importância relativa do processamento contínuo da sessão atual se for bloqueada com outra sessão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
SET DEADLOCK_PRIORITY { LOW | NORMAL | HIGH | <numeric-priority> | @deadlock_var | @deadlock_intvar }  
  
<numeric-priority> ::= { -10 | -9 | -8 | ... | 0 | ... | 8 | 9 | 10 }  
```  
  
## <a name="arguments"></a>Argumentos  
 LOW  
 Especifica que a sessão atual será a vítima de deadlock se estiver envolvida em deadlock e outras sessões envolvidas na cadeia de deadlock tiverem prioridade de deadlock definida como NORMAL ou HIGH ou para um valor de inteiro superior a -5. A sessão atual não será vítima de deadlock se outras sessões forem definidas como prioridade de deadlock como um valor inteiro inferior a -5. Ela também especifica que a sessão atual é elegível para ser vítima de deadlock se outra sessão tiver sido definida com prioridade de deadlock LOW ou um valor inteiro igual a -5.  
  
 NORMAL  
 Especifica que a sessão atual será a vítima de deadlock se outras sessões envolvidas na cadeia de deadlock tiverem prioridade de deadlock definida como HIGH ou para um valor de inteiro superior a 0, mas não será vítima de deadlock se outras sessões estiverem definidas com prioridade de deadlock LOW ou valor inteiro inferior a 0. Ela também especifica que a sessão atual é elegível para ser vítima de deadlock se outra sessão tiver sido definida com prioridade de deadlock NORMAL ou um valor inteiro igual a 0. NORMAL é a prioridade padrão.  
  
 HIGH  
 Especifica que a sessão atual será a vítima de deadlock se outras sessões envolvidas na cadeia de deadlock tiverem prioridade de deadlock definida como um valor de inteiro superior a 5 ou é elegível como vítima de deadlock se outra sessão tiver sido definida com prioridade de deadlock HIGH ou valor inteiro igual a 5.  
  
 \<numeric-priority>  
 É um intervalo de valor inteiro (-10 a 10) para fornecer 21 níveis de prioridade de deadlock. Especifica que a sessão atual será a vítima de deadlock se outras sessões na cadeia de deadlock estiverem em execução em um valor de prioridade de deadlock superior, mas não será a vítima de deadlock se outras sessões estiverem em execução em um valor de prioridade de deadlock inferior ao valor da sessão atual. Ela também especifica que a sessão atual é elegível para ser vítima de deadlock se outra sessão estiver em execução com um valor de prioridade de deadlock que seja igual ao da sessão atual. LOW mapeia para -5, NORMAL para 0 e HIGH para 5.  
  
 **@** *deadlock_var*  
 É uma variável de caractere que especifica a prioridade de deadlock. A variável deve ser definida como um valor de 'LOW', 'NORMAL' ou 'HIGH'. A variável deve ser grande o suficiente para reter a cadeia de caracteres completa.  
  
 **@** *deadlock_intvar*  
 É uma variável de inteiro que especifica a prioridade de deadlock. A variável deve ser definida como um valor de inteiro no intervalo (-10 a 10).  
  
## <a name="remarks"></a>Comentários  
 Surgem deadlocks quando duas sessões estão aguardando acesso a recursos bloqueados por outra. Quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detecta que duas sessões estão com deadlock, ela soluciona o deadlock escolhendo um das sessões como uma vítima de deadlock. A transação atual da vítima é revertida e a mensagem de erro 1205 de deadlock é retornada ao cliente. Isso libera todos os bloqueios retidos por essa sessão, permitindo que a outra sessão continue.  
  
 A escolha de qual sessão será a vítima de deadlock depende da prioridade de deadlock de cada sessão:  
  
-   Se ambas as sessões tiverem a mesma prioridade de deadlock, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escolhe a sessão que é menos dispendiosa para ser revertida como a vítima de deadlock. Por exemplo, se ambas as sessões tiverem definido sua prioridade de deadlock como HIGH, a instância escolherá como uma vítima a sessão que calcula ser menos dispendiosa para reverter. O custo é determinado comparando o número de bytes de log gravados naquele ponto em cada transação. (Você pode ver esse valor como "Log Utilizado" em um gráfico de deadlock).
  
-   Se as sessões tiverem prioridades de deadlock diferentes, a sessão com a prioridade de deadlock mais baixa será escolhida como a vítima de deadlock.  
  
 SET DEADLOCK_PRIORITY é definida ao executar ou no tempo de execução e não no tempo da análise.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa uma variável para definir a prioridade de deadlock como `LOW`.  
  
```sql
DECLARE @deadlock_var NCHAR(3);  
SET @deadlock_var = N'LOW';  
  
SET DEADLOCK_PRIORITY @deadlock_var;  
GO  
```  
  
 O exemplo a seguir define a prioridade de deadlock como `NORMAL`.  
  
```sql
SET DEADLOCK_PRIORITY NORMAL;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [@@LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/functions/lock-timeout-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET LOCK_TIMEOUT &#40;Transact-SQL&#41;](../../t-sql/statements/set-lock-timeout-transact-sql.md)  
  
  
