---
description: sys.database_mirroring_endpoints (Transact-SQL)
title: sys.database_mirroring_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring_endpoints_TSQL
- database_mirroring_endpoints
- sys.database_mirroring_endpoints
- database_mirroring_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], endpoint
- HADR [SQL Server], endpoint
- database mirroring [SQL Server], catalog views
- sys.database_mirroring_endpoints catalog view
ms.assetid: f2285199-97ad-473c-a52d-270044dd862b
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 4e70bd703e258d8605563119e41617985bb0b961
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98093191"
---
# <a name="sysdatabase_mirroring_endpoints-transact-sql"></a>sys.database_mirroring_endpoints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém uma linha para o banco de dados que reflete o ponto de extremidade de uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  O ponto de extremidade de espelhamento de banco de dados dá suporte a ambas as sessões entre parceiros de espelhamento de banco de dados e com testemunhas e sessões entre a réplica primária de um grupo de disponibilidade Always On e suas réplicas secundárias.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|-|Herda colunas de **pontos sys.** end(para obter mais informações, consulte os [pontos de extremidade &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md)).|  
|**role**|**tinyint**|Função de reflexão; uma dentre:<br /><br /> **0** = nenhum<br /><br /> **1** = parceiro<br /><br /> **2** = testemunha<br /><br /> **3** = todos<br /><br /> Observação: esse valor é relevante apenas para espelhamento de banco de dados.|  
|**role_desc**|**nvarchar(60)**|Descrição da função de reflexão; uma dentre:<br /><br /> **NONE**<br /><br /> **PARCEIRO**<br /><br /> **TESTEMUNHA**<br /><br /> **ALL**<br /><br /> Observação: esse valor é relevante apenas para espelhamento de banco de dados.|  
|**is_encryption_enabled**|**bit**|**1** significa que a criptografia está habilitada.<br /><br /> **0** significa que a criptografia está desabilitada.|  
|**connection_auth**|**tinyint**|O tipo de autenticação de conexão exigido para conexões com este ponto de extremidade; um dentre:<br /><br /> **1** -NTLM<br /><br /> **2** -Kerberos<br /><br /> **3** -negociar<br /><br /> **4** -certificado<br /><br /> **5** -NTLM, certificado<br /><br /> **6** -Kerberos, certificado<br /><br /> **7** -negociar, certificado<br /><br /> **8** -certificado, NTLM<br /><br /> **9** -certificado, Kerberos<br /><br /> **10** -Certificate, Negotiate|  
|**connection_auth_desc**|**Nvarchar (60)**|Descrição do tipo de autenticação de conexão exigido para conexões com este ponto de extremidade; uma dentre:<br /><br /> NTLM<br /><br /> KERBEROS<br /><br /> NEGOTIATE<br /><br /> CERTIFICATE<br /><br /> NTLM, CERTIFICATE<br /><br /> KERBEROS, CERTIFICATE<br /><br /> NEGOTIATE, CERTIFICATE<br /><br /> CERTIFICATE, NTLM<br /><br /> CERTIFICATE, KERBEROS<br /><br /> CERTIFICATE, NEGOTIATE|  
|**certificate_id**|**int**|ID de certificado usado para autenticação, se houver.<br /><br /> 0 = Está sendo usada a Autenticação do Windows.|  
|**encryption_algorithm**|**tinyint**|Algoritmo de criptografia; um dentre:<br /><br /> **0** -nenhum<br /><br /> **1** -RC4<br /><br /> **2** -AES<br /><br /> **3** -nenhum, RC4<br /><br /> **4** -nenhum, AES<br /><br /> **5** -RC4, AES<br /><br /> **6** -AES, RC4<br /><br /> **7** -nenhum, RC4, AES<br /><br /> **8** -nenhum, AES, RC4|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Descrição do algoritmo de criptografia; uma dentre:<br /><br /> NONE<br /><br /> RC4<br /><br /> AES<br /><br /> NONE, RC4<br /><br /> NONE, AES<br /><br /> RC4, AES<br /><br /> AES, RC4<br /><br /> NONE, RC4, AES<br /><br /> NONE, AES, RC4|  
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]  
>  O algoritmo RC4 tem suporte somente para compatibilidade com versões anteriores. O novo material só pode ser criptografado por meio do algoritmo RC4 ou RC4_128 quando o banco de dados está no nível de compatibilidade 90 ou 100. (Não recomendável.) Use um algoritmo mais recente; por exemplo, um dos algoritmos AES. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e superior, o material criptografado usando RC4 ou RC4_128 pode ser descriptografado em qualquer nível de compatibilidade.  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Especifique a URL do ponto de extremidade ao adicionar ou modificar uma réplica de disponibilidade &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)   
 [sys.availability_replicas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-availability-replicas-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.database_mirroring ](../../relational-databases/system-catalog-views/sys-database-mirroring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.database_mirroring_witnesses ](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [O ponto de extremidade de espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
