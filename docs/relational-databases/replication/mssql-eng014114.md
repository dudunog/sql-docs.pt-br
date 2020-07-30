---
title: MSSQL_ENG014114 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014114 error
ms.assetid: f5f04590-e1c6-40d8-ab2b-98c791a0fc44
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 5082e524089979ceb6c027073a63a55dd1e5bba0
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87362721"
---
# <a name="mssql_eng014114"></a>MSSQL_ENG014114
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|14114|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|'%s' não está configurado como um Distributor.|  
  
## <a name="explanation"></a>Explicação  
 Se a mensagem de erro especificar uma instância em particular diferente de 'null', a instância especificada não foi configurada corretamente para ser reconhecida como um Distribuidor.  
  
 Se a mensagem especificar 'null' como um Distribuidor, não haverá entrada para o servidor local no banco de dados **mestre** ou a entrada estará incorreta (talvez porque o computador foi renomeado). A replicação espera que todos os servidores em uma topologia sejam registrados usando o nome do computador com um nome da instância opcional (no caso de uma instância clusterizada, o nome do servidor virtual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o nome da instância opcional). Para que a replicação funcione corretamente, o valor retornado pelo `SELECT @@SERVERNAME` para cada servidor na topologia deve corresponder ao nome do computador ou ao nome do servidor virtual com o nome da instância opcional.  
  
 Não haverá suporte para replicação se você tiver registrado qualquer uma das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pelo endereço IP ou FQDN (nome de domínio totalmente qualificado). Se você tinha qualquer das instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registrada pelo endereço IP ou FQDN no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] quando configurou a replicação, esse erro pode ocorrer.  
  
## <a name="user-action"></a>Ação do usuário  
 Se a mensagem de erro especificar uma instância em particular, configure o servidor como um Distribuidor. Para obter mais informações, consulte [Configure Distribution](../../relational-databases/replication/configure-distribution.md).  
  
 Se a mensagem não especificar uma instância em particular ('null'), certifique-se de que a instância do Distribuidor esteja registrada corretamente. Se o nome de rede do computador e o nome da instância do SQL Server forem diferentes:  
  
-   Adicione o nome da instância do SQL Server como um nome de rede válido. Um método para definir um nome de rede alternativo é adicionar isto ao arquivo de hosts local. O arquivo de hosts local fica por padrão situado em WINDOWS\system32\drivers\etc ou WINNT\system32\drivers\etc. Para obter mais informações, consulte a documentação do Windows.  
  
     Por exemplo, se o nome do computador for comp1 e o computador possui um endereço IP 10.193.17.129, e o nome de instância for inst1/instname, adicione a entrada a seguir para os arquivos de host:  
  
     10.193.17.129 inst1  
  
-   Desabilite a distribuição, registre a instância e restabeleça a distribuição. Se o valor @@SERVERNAME não estiver correto em uma instância não clusterizada, siga estas etapas:  
  
    ```  
    sp_dropserver '<old_name>', 'droplogins'  
    go  
    sp_addserver '<new_name>', 'local'  
    go  
    ```  
  
     Depois de executar o procedimento armazenado [sp_addserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), você deverá reiniciar o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que a alteração no @@SERVERNAME entre em vigor.  
  
     Se o valor @@SERVERNAME não estiver correto em uma instância clusterizada, você deverá alterar o nome usando o Administrador de Cluster. Para obter mais informações, consulte [Instâncias de cluster de failover Sempre ativo (SQL Server)](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
