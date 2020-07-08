---
title: catalog.operation_messages (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
helpviewer_keywords:
- catalog.operation_messages view [Integration Services]
- operation_messages view [Integration Services]
ms.assetid: 0b3cbe38-ce24-47ca-83ef-6538a5299d1a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 05fb06f9e15557628f37d0bc6c113606f04dd19b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85671881"
---
# <a name="catalogoperation_messages-ssisdb-database"></a>catalog.operation_messages (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Exibe mensagens que são registradas em log durante operações no catálogo do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|operation_message_id|**bigint**|O ID (identificador exclusivo) da mensagem.|  
|operation_id|**bigint**|A ID exclusiva da operação.|  
|message_time|**datetimeoffset(7)**|A hora em que a mensagem foi criada.|  
|message_type|**smallint**|O tipo da mensagem exibida.|  
|message_source_type|**smallint**|A ID do tipo de origem da mensagem.|  
|message|**nvarchar(max)**|O texto da mensagem.|  
|extended_info_id|**bigint**|A ID de informações adicionais relacionadas à mensagem da operação, localizada na exibição [extended_operation_info](../../integration-services/system-views/catalog-extended-operation-info-ssisdb-database.md).|  
  
## <a name="remarks"></a>Comentários  
 Essa exibição exibe uma linha para cada mensagem registrada durante uma operação no catálogo. A mensagem pode ser gerada pelo servidor, pelo processo de execução do pacote ou pelo mecanismo de execução.  
  
 Esta exibição exibe os tipos de mensagem a seguir:  
  
|Valor **message_type**|DESCRIÇÃO|  
|-----------------------------|-----------------|  
|-1|Unknown (desconhecido)|  
|120|Erro|  
|110|Aviso|  
|70|Informações|  
|10|Pré-validar|  
|20|Pós-validar|  
|30|Pré-executar|  
|40|Pós-executar|  
|60|Andamento|  
|50|StatusChange|  
|100|QueryCancel|  
|130|TaskFailed|  
|90|Diagnostic|  
|200|Personalizado|  
|140|DiagnosticEx<br /><br /> Sempre que uma tarefa Executar Pacote executa um pacote filho, ela registra esse evento. A mensagem de evento consiste nos valores de parâmetros passados para pacotes filho.<br /><br /> O valor da coluna de mensagem para DiagnosticEx é texto XML.|  
|400|NonDiagnostic|  
|80|VariableValueChanged|  
  
 Esta exibição exibe os tipos de origem de mensagem a seguir.  
  
|**message_source_type**|DESCRIÇÃO|  
|-------------------------------|-----------------|  
|10|APIs de entrada, como os procedimentos armazenados T-SQL e CLR|  
|20|O processo externo usado para executar pacote (ISServerExec.exe)|  
|30|Objetos de nível de pacote|  
|40|Tarefas de fluxo de controle|  
|50|Contêineres de fluxo de controle|  
|60|Tarefa de Fluxo de Dados|  
  
## <a name="permissions"></a>Permissões  
 Esta exibição requer uma das seguintes permissões:  
  
-   Permissão READ na operação  
  
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
  
> [!NOTE]  
>  Quando você tem permissão para executar uma operação no servidor, também tem permissão para exibir informações sobre a operação. A segurança em nível de linha é imposta; somente as linhas para as quais você tem permissão de exibição são exibidas.  
  
  
