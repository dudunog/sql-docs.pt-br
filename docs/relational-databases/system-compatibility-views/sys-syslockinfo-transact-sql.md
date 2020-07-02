---
title: sys.syslockinfo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syslockinfo_TSQL
- sys.syslockinfo_TSQL
- sys.syslockinfo
- syslockinfo
dev_langs:
- TSQL
helpviewer_keywords:
- syslockinfo system table
- sys.syslockinfo compatibility view
ms.assetid: d8cae434-807a-473e-b94f-f7a0e1b2daf0
author: rothja
ms.author: jroth
ms.openlocfilehash: 90573a28292ac4f4de973dc2a5a0c5e1f331d2f0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764389"
---
# <a name="syssyslockinfo-transact-sql"></a>sys.syslockinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Contém informações sobre todas as solicitações de bloqueios concedidas, de conversão e em espera.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
> [!IMPORTANT]  
>  Esse recurso foi alterado em relação às versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [alterações recentes em recursos de mecanismo de banco de dados no SQL Server 2016](../../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**rsc_text**|**nchar(32)**|Descrição textual de um recurso de bloqueio. Contém uma parte do nome de recurso.|  
|**rsc_bin**|**binary(16)**|Recurso de bloqueio binário. Contém o recurso de bloqueio real que está contido no administrador de bloqueio. Essa coluna está incluída para ferramentas que conhecem o formato de recurso de bloqueio para gerar seu próprio recurso de bloqueio formatado e para executar autojunções em **syslockinfo**.|  
|**rsc_valblk**|**binary(16)**|Bloco de valor de bloqueio. Alguns tipos do recurso podem incluir dados adicionais no recurso de bloqueio sem-hash do administrador de bloqueio para determinar a propriedade de um recurso de bloqueio específico. Por exemplo, bloqueios de página não pertencem a um ID de objeto específico. Para escalonamento de bloqueios e outros fins. Porém, o ID de objeto de um bloqueio de página pode ser incluído no bloco de valor de bloqueio.|  
|**rsc_dbid**|**smallint**|ID de banco de dados associado ao recurso.|  
|**rsc_indid**|**smallint**|ID de índice associado com o recurso, se apropriado.|  
|**rsc_objid**|**int**|ID de objeto associado com o recurso, se apropriado.|  
|**rsc_type**|**tinyint**|Tipo de recurso:<br /><br /> 1 = Recurso NULL (não usado)<br /><br /> 2 = banco de dados<br /><br /> 3 = Arquivo<br /><br /> 4 = Índice<br /><br /> 5 = Tabela<br /><br /> 6 = Página<br /><br /> 7 = Chave<br /><br /> 8 = Extensão<br /><br /> 9 = RID (ID de linha)<br /><br /> 10 = Aplicativo|  
|**rsc_flag**|**tinyint**|Sinalizadores de recursos internos.|  
|**req_mode**|**tinyint**|Modo de solicitação de bloqueio. Esta coluna é o modo de bloqueio do solicitador e representa ou o modo concedido, convertido ou o  modo de espera.<br /><br /> 0 = NULL. Nenhum acesso concedido ao recurso. Funciona como espaço reservado.<br /><br /> 1 = Sch-S (Estabilidade do esquema). Assegura que um elemento de esquema, como uma tabela ou índice, não seja cancelado enquanto qualquer sessão mantém o bloqueio de estabilidade do esquema no elemento do esquema.<br /><br /> 2 = Sch-M (Modificação do esquema). Deve ser mantido por qualquer sessão que desejar alterar o esquema do recurso especificado. Assegura que nenhuma outra sessão esteja fazendo referência ao objeto indicado.<br /><br /> 3 = S (Compartilhado). A sessão mantenedora possui acesso compartilhado ao recurso.<br /><br /> 4 = U (Atualização). Indica um bloqueio de atualização adquirido em recursos que podem ser atualizados eventualmente. É usado para evitar uma forma comum de deadlock que ocorre quando várias sessões bloqueiam recursos para uma atualização potencial no futuro.<br /><br /> 5 = X (Exclusivo). A sessão mantenedora possui acesso exclusivo ao recurso.<br /><br /> 6 = IS (Compartilhamento intencional). Indica a intenção de colocar bloqueios S em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> 7 = IU (Atualização intencional). Indica a intenção de colocar bloqueios U em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> 8 = IX (Exclusivo intencional). Indica a intenção de colocar bloqueios X em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> 9 = SIU (Atualização intencional compartilhada). Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios de atualização em recursos subordinados na hierarquia de bloqueio.<br /><br /> 10 = SIX (Exclusivo intencional de compartilhamento). Indica o acesso compartilhado a um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.<br /><br /> 11 = UIX (Exclusivo intencional de atualização). Indica a manutenção de um bloqueio de atualização de um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.<br /><br /> 12 = BU. Usado por operações em massa.<br /><br /> 13 = RangeS_S (Intervalo de chave compartilhada e bloqueio de recurso compartilhado). Indica varredura de intervalo serializável.<br /><br /> 14 = RangeS_U (Intervalo de chave compartilhada e bloqueio de recurso de atualização). Indica verificação de atualização serializável.<br /><br /> 15 = RangeI_N (Intervalo de chave de inserção e bloqueio de recurso nulo). Usado para testar intervalos antes de inserir uma nova chave em um índice.<br /><br /> 16 = RangeI_S. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e S.<br /><br /> 17 = RangeI_U. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e U.<br /><br /> 18 = RangeI_X. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e X.<br /><br /> 19 = RangeX_S. Bloqueio de conversão de intervalo de chaves criado por uma sobreposição de bloqueios RangeI_N e RangeS-S.<br /><br /> 20 = RangeX_U. Bloqueio de conversão de intervalo de chave criado por uma sobreposição dos bloqueios RangeI_N e RangeS_U.<br /><br /> 21 = RangeX_X (Bloqueio de intervalo de chave exclusivo e de recurso exclusivo). Este é um bloqueio de conversão usado na atualização de uma chave em um intervalo.|  
|**req_status**|**tinyint**|O status de solicitação do bloqueio:<br /><br /> 1 = concedido<br /><br /> 2 = convertendo<br /><br /> 3 = aguardando|  
|**req_refcnt**|**smallint**|Contagem de referência de bloqueio. Sempre que uma transação solicita um bloqueio em um recurso específico, uma conta de referência é incrementada. O bloqueio não pode ser liberado até que a contagem de referência seja igual a 0.|  
|**req_cryrefcnt**|**smallint**|Reservado para uso futuro. Sempre defina em 0.|  
|**req_lifetime**|**int**|Bitmap de tempo de vida de bloqueio. Durante certas estratégias de processamento de consulta, devem ser mantidos os bloqueios nos recursos até que o processador de consulta complete uma fase específica da consulta. O bitmap de tempo de vida de bloqueio é usado pelo processador de consulta e gerenciador de transações  para indicar grupos de bloqueios que podem ser liberados quando uma determinada fase de uma consulta terminar sua execução. São usados certos bits no bitmap para indicar bloqueios que são mantidos até o término de uma transação, até mesmo se a contagem de referência for igual a 0.|  
|**req_spid**|**int**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ID de processo interno da sessão que solicita o bloqueio.|  
|**req_ecid**|**int**|ID de contexto de execução (ECID). Usado para indicar qual thread em uma operação paralela possui um bloqueio específico.|  
|**req_ownertype**|**smallint**|Tipo de objeto associado com o bloqueio:<br /><br /> 1 = Transação<br /><br /> 2 = Cursor<br /><br /> 3 = Sessão<br /><br /> 4 = ExSessão<br /><br /> Note que 3 e 4 representam uma versão especial de bloqueios de sessão, controle de banco de dados e bloqueios de grupos de arquivos respectivamente.|  
|**req_transactionID**|**bigint**|ID de transação exclusiva usada em **syslockinfo** e no evento do criador de perfil|  
|**req_transactionUOW**|**uniqueidentifier**|Identifica o ID de unidade de trabalho (UOW) da transação de DTC. Para transações de DTC não MS, o UOW é definido em 0.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Mapeando tabelas do sistema para exibições do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
