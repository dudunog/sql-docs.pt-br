---
description: '&#x40;&#x40;OPTIONS (Transact-SQL)'
title: '@@OPTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@OPTIONS'
- '@@OPTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- SET statement, current SET options
- '@@OPTIONS function'
- current SET options
ms.assetid: 3d5c7f6e-157b-4231-bbb4-4645a11078b3
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: aba9b19dd9788eef4f322db198dd7f8f3789a8c8
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128391"
---
# <a name="x40x40options-transact-sql"></a>&#x40;&#x40;OPTIONS (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna informações sobre as opções SET atuais.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
@@OPTIONS  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 **inteiro**  
  
## <a name="remarks"></a>Comentários  
 As opções podem ser obtidas do uso do comando **SET** ou do valor das **opções de usuário de sp_configure**. Os valores de sessão configurados com o comando **SET** substituem as opções de **sp_configure**. Muitas ferramentas (tal como [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]) configuram automaticamente as opções do conjunto. Cada usuário tem uma função @@OPTIONS que representa a configuração.  
  
 Você pode alterar as opções de idioma e de processamento de consulta para uma sessão de usuário específico usando a instrução SET. **\@\@OPTIONS** só pode detectar as opções que estão definidas como ON ou OFF.  
  
 A função **\@\@OPTIONS** retorna um bitmap das opções, convertidas em um inteiro de base 10 (decimal). As configurações de bits são armazenadas nas localizações descritas em uma tabela no tópico [Configurar a opção user options de configuração do servidor](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md).  
  
 Para decodificar o valor **\@\@OPTIONS**, converta o inteiro retornado por **\@\@OPTIONS** em binário e, em seguida, examine os valores na tabela em [Configurar a opção user options de configuração do servidor](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md). Por exemplo, se `SELECT @@OPTIONS;` retornar o valor de `5496`, use a calculadora do programador do Windows (**calc.exe**) para converter o decimal `5496` em binário. O resultado é `1010101111000`. Os caracteres mais à direita (binário 1, 2 e 4) são 0, indicando que os primeiros três itens da tabela estão desativados. Consultando a tabela, você verá que eles são **DISABLE_DEF_CNST_CHK**, **IMPLICIT_TRANSACTIONS**, e **CURSOR_CLOSE_ON_COMMIT**. O próximo item (**ANSI_WARNINGS** na posição `1000`) está ativado. Continue trabalhando à direita pelo bitmap e para baixo na lista de opções. Quando as opções mais à esquerda forem 0, elas serão truncadas pela conversão de tipo. O bitmap `1010101111000` é na verdade `001010101111000` para representar todas as 15 opções.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-demonstration-of-how-changes-affect-behavior"></a>a. Demonstração de como as alterações afetam o comportamento  
 O exemplo a seguir demonstra a diferença no comportamento de concatenação com duas configurações diferentes da opção **CONCAT_NULL_YIELDS_NULL**.  
  
```sql  
SELECT @@OPTIONS AS OriginalOptionsValue;  
SET CONCAT_NULL_YIELDS_NULL OFF;  
SELECT 'abc' + NULL AS ResultWhen_OFF, @@OPTIONS AS OptionsValueWhen_OFF;  
  
SET CONCAT_NULL_YIELDS_NULL ON;  
SELECT 'abc' + NULL AS ResultWhen_ON, @@OPTIONS AS OptionsValueWhen_ON;  
```  
  
### <a name="b-testing-a-client-nocount-setting"></a>B. Testando uma configuração de cliente NOCOUNT  
 O exemplo a seguir define `NOCOUNT``ON` e, em seguida, e testa o valor de `@@OPTIONS`. A opção `NOCOUNT``ON` impede que a mensagem sobre o número de linhas afetadas seja enviada novamente ao cliente solicitante para cada instrução em uma sessão. O valor de `@@OPTIONS` é definido como `512` (0x0200). Isto representa a opção NOCOUNT. Este exemplo testa se a opção NOCOUNT está habilitada no cliente. Por exemplo, isso pode ajudar a controlar diferenças de desempenho em um cliente.  
  
```sql  
SET NOCOUNT ON  
IF @@OPTIONS & 512 > 0   
RAISERROR ('Current user has SET NOCOUNT turned on.', 1, 1)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Configurar as opções de configuração de servidor user connections](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)  
  
  
