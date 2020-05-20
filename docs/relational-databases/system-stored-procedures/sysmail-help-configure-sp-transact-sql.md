---
title: sysmail_help_configure_sp (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sysmail_help_configure_sp
- sysmail_help_configure_sp_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmail_help_configure_sp
ms.assetid: e598d4c8-3041-4965-b046-dce3a8e3d3e0
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8a29933568cec147dc27ff7c9b5f026d62856e5b
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82807697"
---
# <a name="sysmail_help_configure_sp-transact-sql"></a>sysmail_help_configure_sp (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Exibe definições de configuração do Database Mail.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sysmail_help_configure_sp  [ [ @parameter_name = ] 'parameter_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @parameter_name = ] 'parameter_name'`O nome da definição de configuração a ser recuperada. Quando especificado, o valor da definição de configuração é retornado no parâmetro de saída ** \@ parameter_value** . Quando nenhum ** \@ parameter_name** é especificado, esse procedimento armazenado retorna um conjunto de resultados que contém todas as definições de configuração de Database Mail na instância.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Quando nenhum ** \@ parameter_name** for especificado, o retornará um conjunto de resultados com as colunas a seguir.  
  
||||  
|-|-|-|  
|Nome da coluna|Tipo de dados|Descrição|  
|**paramName**|**nvarchar(256)**|O nome do parâmetro de configuração.|  
|**ParamValue**|**nvarchar(256)**|O valor do parâmetro de configuração.|  
|**ndescrição**|**nvarchar(256)**|A descrição do parâmetro de configuração.|  
  
## <a name="remarks"></a>Comentários  
 O procedimento armazenado **sysmail_help_configure_sp** lista as definições de configuração de Database Mail atuais para a instância do.  
  
 Quando um ** \@ parameter_name** é especificado, mas nenhum parâmetro de saída é fornecido para ** \@ parameter_value**, esse procedimento armazenado não produz nenhuma saída.  
  
 O procedimento armazenado **sysmail_help_configure_sp** está no banco de dados **msdb** e pertence ao esquema **dbo** . O procedimento deve ser chamado com um nome de três partes se o banco de dados atual não for **msdb**.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução para este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra a listagem das definições de configuração do Database Mail para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXECUTE msdb.dbo.sysmail_help_configure_sp ;  
```  
  
 Conjunto de resultados de exemplo, editado para comprimento de linha:  
  
```  
paramname                       paramvalue      description  
------------------------------- --------------- -----------------------------------------------------------------------------  
AccountRetryAttempts            1               Number of retry attempts for a mail server  
AccountRetryDelay               5000            Delay between each retry attempt to mail server  
DatabaseMailExeMinimumLifeTime  600             Minimum process lifetime in seconds  
DefaultAttachmentEncoding       MIME            Default attachment encoding  
LoggingLevel                    2               Database Mail logging level: normal - 1, extended - 2 (default), verbose - 3  
MaxFileSize                     1000000         Default maximum file size  
ProhibitedExtensions            exe,dll,vbs,js  Extensions not allowed in outgoing mails  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Database Mail](../../relational-databases/database-mail/database-mail.md)   
 [Database Mail procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)  
  
  
