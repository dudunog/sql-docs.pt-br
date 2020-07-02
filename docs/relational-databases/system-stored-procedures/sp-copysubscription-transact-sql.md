---
title: sp_copysubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_copysubscription
- sp_copysubscription_TSQL
helpviewer_keywords:
- sp_copysubscription
ms.assetid: 3c56cd62-2966-4e87-a986-44cb3fd0b760
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 80927c19376e97b25c21af1f93faedd5637eb8bb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771203"
---
# <a name="sp_copysubscription-transact-sql"></a>sp_copysubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

    
> [!IMPORTANT]  
>  O recurso de assinaturas anexáveis está preterido e será removido em uma versão futura. Esse recurso não deveria ser usado em novo trabalho de desenvolvimento. Para publicações de mesclagem, que são particionadas usando filtros com parâmetros, recomendamos o uso de novos recursos de instantâneos particionados, que simplificam a inicialização de um grande número de assinaturas. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). Para publicações que não são particionadas, é possível inicializar uma inscrição com um backup. Para obter mais informações, consulte [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md).  
  
 Copia um banco de dados de assinatura que tem assinatura pull, mas nenhuma assinatura push. Somente bancos de dados de arquivo único podem ser copiados. Esse procedimento armazenado é executado no Assinante no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_copysubscription [ @filename = ] 'file_name'  
    [ , [ @temp_dir = ] 'temp_dir' ]  
    [ , [ @overwrite_existing_file = ] overwrite_existing_file]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @filename = ] 'file_name'`É a cadeia de caracteres que especifica o caminho completo, incluindo o nome do arquivo, para o qual uma cópia do arquivo de dados (. MDF) é salva. o *nome do arquivo* é **nvarchar (260)**, sem padrão.  
  
`[ @temp_dir = ] 'temp_dir'`É o nome do diretório que contém os arquivos temporários. *temp_dir* é **nvarchar (260)**, com um padrão de NULL. Se for NULL, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretório de dados padrão será usado. O diretório deve ter bastante espaço suficiente para conter um arquivo do tamanho de todos os arquivos de banco de dados de assinante combinados.  
  
`[ @overwrite_existing_file = ] 'overwrite_existing_file'`É um sinalizador booliano opcional que especifica se deve ou não substituir um arquivo existente com o mesmo nome especificado em ** \@ filename**. *overwrite_existing_file*é **bit**, com um padrão de **0**. Se for **1**, ele substituirá o arquivo especificado por ** \@ filename**, se existir. Se **0**, o procedimento armazenado falhará se o arquivo existir e o arquivo não for substituído.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_copysubscription** é usado em todos os tipos de replicação para copiar um banco de dados de assinatura para um arquivo como uma alternativa para aplicar um instantâneo no Assinante. O banco de dados deve ser configurado para oferecer suporte somente a assinaturas pull. Usuários com permissões apropriadas podem fazer cópias do banco de dados de assinatura e enviar por email, copiar ou transportar o arquivo de assinatura (.msf) para outro Assinante, onde poderá ser anexado a uma assinatura.  
  
 O tamanho do banco de dados de assinatura copiado deve ser menor de 2 gigabytes (GB).  
  
 Só há suporte para **sp_copysubscription** para bancos de dados com assinaturas de cliente e não pode ser executado quando o banco de dados tem assinaturas de servidor.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** podem executar **sp_copysubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Locais de pastas de instantâneos alternativos](../../relational-databases/replication/snapshot-options.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
