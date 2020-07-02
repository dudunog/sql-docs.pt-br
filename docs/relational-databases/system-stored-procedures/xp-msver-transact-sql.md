---
title: xp_msver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_msver_TSQL
- xp_msver
dev_langs:
- TSQL
helpviewer_keywords:
- xp_msver
ms.assetid: 9264cf8c-92ba-45ad-b2d6-15d26d805a16
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 385bae0bd40fd392f038ef4dd85204c853a81773
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762630"
---
# <a name="xp_msver-transact-sql"></a>xp_msver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações de versão sobre [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **xp_msver** também retorna informações sobre o número de Build real do servidor e informações sobre o ambiente de servidor. As informações que **xp_msver** retorna podem ser usadas em [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções, lotes, procedimentos armazenados e assim por diante, para aprimorar a lógica para o código independente de plataforma.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xp_msver [ optname ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *optname*  
 É o nome de uma opção e pode ter um dos valores a seguir.  
  
|Opção/Nome da coluna|Description|  
|-------------------------|-----------------|  
|**NomeDoProduto**|Nome do produto; por exemplo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**ProductVersion**|Versão do produto.|  
|**Idioma**|A versão do idioma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Plataforma**|Nome do sistema operacional, nome do fabricante e nome da família do chip para o computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Comentários**|Informações diversas sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**CompanyName**|Nome da empresa que produz o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; por exemplo,  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation.|  
|**FileDescription**|O sistema operacional.|  
|**FileVersion**|Versão do executável do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**InternalName**|Nome interno da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; por exemplo, SQLSERVR.|  
|**LegalCopyright**|Informações legais sobre direitos autorais exigidas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; por exemplo, Copyright© [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corp. 1988-2005.|  
|**LegalTrademarks**|Informações legais sobre marca comercial exigidas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por exemplo, [!INCLUDE[msCoName](../../includes/msconame-md.md)] é uma marca comercial registrada da [!INCLUDE[msCoName](../../includes/msconame-md.md)] Corporation.|  
|**OriginalFilename**|Nome de arquivo executado na inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; por exemplo, Sqlservr.exe.|  
|**PrivateBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**SpecialBuild**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**WindowsVersion**|Versão do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows instalada no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ProcessorCount**|O número de processadores no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ProcessorActiveMask**|Indica os processadores instalados no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são iniciados e utilizados pelo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.|  
|**ProcessorType**|Tipo de processador. Semelhante à **plataforma**.|  
|**PhysicalMemory**|Quantidade em megabytes (MB) de RAM instalada no computador que está executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**ID do Produto**|Identificação do produto (Product ID). É especificada durante a instalação. Esse número está localizado em um adesivo no estojo do CD original do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 1 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **xp_msver**, sem nenhum parâmetro, retorna um conjunto de resultados de quatro colunas que lista todos os valores de opção. **xp_msver**, para qualquer parâmetro, retorna o conjunto de resultados de quatro colunas com valores para essa opção.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados estendidos gerais &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [@@VERSION &#40;Transact-SQL&#41;](../../t-sql/functions/version-transact-sql-configuration-functions.md)  
  
  
