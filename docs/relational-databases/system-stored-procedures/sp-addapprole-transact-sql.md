---
title: sp_addapprole (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addapprole_TSQL
- sp_addapprole
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addapprole
ms.assetid: 24200295-9a54-4cab-9922-fb2e88632721
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 74860a8f4c8dee263ea7ee0eea75679c721d1fa5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68032983"
---
# <a name="sp_addapprole-transact-sql"></a>sp_addapprole (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma função de aplicativo ao banco de dados atual.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Em vez disso, use [criar função de aplicativo](../../t-sql/statements/create-application-role-transact-sql.md) .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addapprole [ @rolename = ] 'role' , [ @password = ] 'password'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @rolename = ] 'role'`É o nome da nova função de aplicativo. *role* é **sysname**, sem padrão. a *função* deve ser um identificador válido e já não pode existir no banco de dados atual.  
  
 Os nomes de função de aplicativo podem conter de 1 até 128 caracteres, inclusive cartas, símbolos e números. Os nomes de função não podem conter uma\\barra invertida () nem ser nulo ou uma cadeia de caracteres vazia (' ').  
  
`[ @password = ] 'password'`É a senha necessária para ativar a função de aplicativo. a *senha* é **sysname**, sem padrão. a *senha* não pode ser nula.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 Em versões anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], os usuários (e as funções) não são completamente distintos de esquemas. Começando com [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os esquemas são completamente distintos de funções. Esta nova arquitetura é refletida no comportamento de CREATE APPLICATION ROLE. Essa instrução substitui **sp_addapprole**.  
  
 Para manter a compatibilidade com versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], **sp_addapprole** fará o seguinte:  
  
-   Se um esquema de nome igual ao da função de aplicativo ainda não existir, tal esquema será criado. O novo esquema será de propriedade da função de aplicativo e será o esquema padrão da função de aplicativo.  
  
-   Se um esquema de nome igual ao da função de aplicativo já existir, o procedimento falhará.  
  
-   A complexidade da senha não é verificada por **sp_addapprole**. Mas a complexidade da senha é verificada por CREATE APPLICATION ROLE.  
  
 A *senha* do parâmetro é armazenada como um hash unidirecional.  
  
 Não é possível executar o procedimento armazenado **sp_addapprole** de dentro de uma transação definida pelo usuário.  
  
> [!IMPORTANT]  
>  A opção Microsoft ODBC **Encrypt** não é suportada pelo **SqlClient**. Quando possível, solicite que os usuários insiram as credenciais de função de aplicativo no momento da execução. Evite armazenar as credenciais em um arquivo. Se precisar manter as credenciais, criptografe-as usando as funções CryptoAPI.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados. Se um esquema com nome e proprietário iguais aos da nova função ainda não existir, isso também exigirá a permissão CREATE SCHEMA no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona a nova função `SalesApp` de aplicativo com `x97898jLJfcooFUYLKm387gf3` a senha para o banco de dados atual.  
  
```  
EXEC sp_addapprole 'SalesApp', 'x97898jLJfcooFUYLKm387gf3' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-application-role-transact-sql.md)  
  
  
