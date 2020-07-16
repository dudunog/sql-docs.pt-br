---
title: Identidade e controle de acesso (Replicação) | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- access controls [SQL Server replication]
- security [SQL Server replication], identity and access control
- authentication [SQL Server replication]
- identity [Replication]
ms.assetid: 4da0e793-1ee4-4f69-a80b-45c6732a238d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 39e0e7edb6b3863b29e5dc4016253fb7c736838d
ms.sourcegitcommit: 21c14308b1531e19b95c811ed11b37b9cf696d19
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86160054"
---
# <a name="identity-and-access-control-replication"></a>Identidade e controle de acesso (Replicação)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/applies-to-version/sql-asdbmi.md)]
  A autenticação é o processo pelo qual uma entidade (geralmente um computador neste contexto) verifica se outra entidade, também chamada *principal*, (geralmente um outro computador ou um usuário) é quem ou o que diz ser. A autorização é o processo pelo qual um principal autenticado obtém acesso aos recursos, como um arquivo no sistema de arquivos ou  uma tabela no banco de dados.  
  
 A segurança de replicação usa a autenticação e a autorização para controlar o acesso aos objetos de banco de dados replicados e aos computadores e agentes envolvidos no processamento de replicação. Isso é realizado por meio de três mecanismos:  
  
-   Segurança do agente  
  
     O modelo de segurança do agente de replicação permite um controle refinado das contas nas quais os agentes de replicação executam e efetuam conexões. Para obter informações detalhadas sobre o modelo de segurança do agente, consulte [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md). 
  
-   Funções de administração  
  
     Certifique-se de que  o servidor e as funções do banco de dados corretos sejam usados na configuração, manutenção e processamento da replicação. Para obter mais informações, consulte [Security Role Requirements for Replication](../../../relational-databases/replication/security/security-role-requirements-for-replication.md).  
  
-   A lista de acesso à publicação (PAL)  
  
     Conceda acesso a publicações por meio da PAL. A PAL funciona de modo semelhante à lista de controle de acesso do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Quando um Assinante se conecta ao Publicador ou ao Distribuidor e solicita acesso à publicação, as informações de autenticação passadas pelo agente são verificadas de acordo com a PAL. Para mais informações e melhores práticas para a PAL, consulte [Proteger o Publicador](../../../relational-databases/replication/security/secure-the-publisher.md).  
  
## <a name="filtering-published-data"></a>Filtrando dados publicados  
 Além de usar a autenticação e a autorização para controlar o acesso aos dados e objetos replicados, a replicação inclui duas opções para controlar quais dados estão disponíveis no Assinante: a filtragem de colunas e a filtragem de linhas. Para mais informações sobre filtragem, consulte [Filtrar dados publicados](../../../relational-databases/replication/publish/filter-published-data.md).  
  
 Ao definir um artigo, você pode publicar apenas as colunas que são necessárias para a publicação e omitir as desnecessárias ou aquelas que contêm dados confidenciais. Por exemplo, quando publicar a tabela **Customer** do banco de dados Adventure Works para os representantes de vendas em atuação na área, você pode omitir a coluna **AnnualSales** , que talvez seja importante apenas para os executivos da empresa.  
  
 A filtragem de dados publicados restringe o acesso aos dados e permite que você especifique os dados disponíveis no Assistente. Por exemplo, você pode filtrar a tabela **Customer** para que os parceiros da corporação recebam apenas as informações sobre os clientes cuja coluna **ShareInfo** tenha um valor de "sim." Para a replicação de mesclagem, haverá considerações de segurança se você usar um filtro com parâmetros que inclua HOST_NAME(). Para obter mais detalhes, consulte a seção "Filtragem com HOST_NAME ()" em [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  

## <a name="manage-logins-and-passwords-in-replication"></a>Gerenciar logons e senhas na replicação
Ao configurar a replicação, especifique os logons e as senhas para agentes de replicação. Depois de configurar a replicação, você pode alterar os logons e as senhas. Para obter mais informações, consulte [View and Modify Replication Security Settings](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md). Se você alterar a senha de uma conta usada por um agente de replicação, execute [sp_changereplicationserverpasswords &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md).  

Suporte para o uso de gMSA (Conta de Serviço Gerenciado de grupo) é introduzido no SQL Server 2014. Para obter mais informações, veja o blog [Replicação e Contas de Serviço Gerenciado de grupo](https://repltalk.com/2019/03/26/replication-and-group-managed-service-accounts/).
  
## <a name="see-also"></a>Consulte Também  
 [Mitigação de ameaça e vulnerabilidade &#40;replicação&#41;](../../../relational-databases/replication/security/threat-and-vulnerability-mitigation-replication.md) [Modelo de segurança do agente de replicação](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   

  
  
