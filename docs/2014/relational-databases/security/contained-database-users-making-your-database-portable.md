---
title: Usuários de banco de dados independentes – transformando seu banco de dados em portátil | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- contained database, users
- user [SQL Server], about contained database users
ms.assetid: e57519bb-e7f4-459b-ba2f-fd42865ca91d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6aef800c41b0c1b44e285f959d1b9e12c58ea937
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997498"
---
# <a name="contained-database-users---making-your-database-portable"></a>Usuários de bancos de dados independentes - Tornando seu banco de dados portátil
  Use usuários de banco de dados independentes para autenticar conexões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)] no nível do banco de dados. Um banco de dados independente é um banco de dados isolado de outros bancos de dados e da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]/[!INCLUDE[ssSDS](../../includes/sssds-md.md)] (e o banco de dados mestre) que hospeda o banco de dados. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a usuários de bancos de dados independentes para autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Windows. Ao usar [!INCLUDE[ssSDS](../../includes/sssds-md.md)], combine usuários do banco de dados com regras de firewall de nível de banco de dados. Este tópico revisa as diferenças e os benefícios de usar o modelo de banco de dados independente em comparação com o modelo de logon/usuário tradicional e Windows ou as regras de firewall em nível de servidor. Cenários específicos, lógica de negócios do aplicativo ou a capacidade de gerenciamento ainda podem exigir o uso do modelo tradicional de logon/usuário e regras de firewall em nível de servidor.  
  
> [!NOTE]  
>  Conforme [!INCLUDE[msCoName](../../includes/msconame-md.md)] causa a evolução do serviço [!INCLUDE[ssSDS](../../includes/sssds-md.md)] e move-o para maiores SLAs garantidos, você talvez precise alternar para o modelo de usuário de banco de dados independente e regras de firewall no escopo do banco de dados para obter o SLA de disponibilidade superior, e taxas mais altas de logon máximo para um determinado banco de dados. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Incentivamos você a considerar essas alterações hoje mesmo.  
  
## <a name="traditional-login-and-user-model"></a>Modelo de usuário e logon tradicional  
 No modelo de conexão tradicional, usuários do Windows ou membros de grupos do Windows se conectem ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] fornecendo credenciais de usuário ou grupo autenticadas pelo Windows. Ou a conexão fornece um nome e uma senha e se conecta usando a autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (que é a única opção ao se conectar ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)]). Em ambos os casos, o banco de dados mestre deve ter um logon que corresponde às credenciais de conexão. Depois que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] confirmar as credenciais de autenticação do Windows ou autenticar as credenciais de autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a conexão normalmente tenta se conectar a um banco de dados do usuário. Para se conectar a um banco de dados do usuário, o logon deve ser capaz de ser mapeado para (ou seja, associado) um usuário de banco de dados no banco de dados do usuário. A cadeia de conexão também pode especificar a conexão com um banco de dados específico que é opcional em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mas obrigatório em [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 A entidade de segurança importante é que o logon (no banco de dados mestre) e o usuário (no banco de dados do usuário) devem existir e estar relacionados entre si. Isso significa que a conexão com o banco de dados do usuário tem uma dependência no momento do logon no banco de dados mestre, e isso limita a capacidade do banco de dados de ser movido para um host [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente ou servidor [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] . E se, por algum motivo, uma conexão com o banco de dados mestre não estiver disponível (por exemplo, um failover está em andamento), o tempo de conexão geral será aumentado ou a conexão poderá atingir o tempo limite. Consequentemente, isso pode reduzir a escalabilidade da conexão.  
  
## <a name="contained-database-user-model"></a>Modelo de usuário de banco de dados independente  
 O logon no banco de dados mestre não está presente no modelo de usuário de banco de dados independente. Em vez disso, o processo de autenticação ocorre no banco de dados do usuário e o usuário no banco de dados não tem um logon associado no banco de dados mestre. O modelo de usuário de banco de dados independente dá suporte à autenticação do Windows (em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) e à autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]). Para se conectar como um usuário de banco de dados independente, a cadeia de conexão sempre deve conter um parâmetro para o banco de dados do usuário para que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] saiba qual banco de dados é responsável por gerenciar o processo de autenticação. A atividade do usuário de banco de dados independente está limitada ao banco de dados responsável pela autenticação. Portanto, ao se conectar como um usuário de banco de dados independente, a conta de usuário do banco de dados deve ser criada independentemente em cada banco de dados de que o usuário precisará. Para alterar os bancos de dados, os usuários [!INCLUDE[ssSDS](../../includes/sssds-md.md)] devem criar uma nova conexão. Os usuários de bancos de dados independentes no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderão alterar bancos de dados se um usuário idêntico estiver presente em outro banco de dados.  
  
 Para o [!INCLUDE[ssSDS](../../includes/sssds-md.md)], nenhuma alteração é necessária na cadeia de conexão ao alternar do modelo tradicional para o modelo de usuário de banco de dados independente. Para conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o nome do banco de dados deve ser adicionado à cadeia de conexão se não ainda estiver presente.  
  
> [!IMPORTANT]  
>  Ao usar o modelo tradicional, as funções de nível de servidor e permissões de nível de servidor podem limitar o acesso a todos os bancos de dados. Ao usar o modelo de banco de dados independente, os proprietários e os usuários do banco de dados a permissão ALTER ANY USER podem conceder acesso ao banco de dados. Isso reduz o controle de acesso dos logons do servidor com privilégios altos e expande o controle de acesso para incluir os usuários do banco de dados com privilégios altos.  
  
## <a name="firewalls"></a>Firewalls  
  
### [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Regras de firewall do Windows se aplicam a todas as conexões e têm os mesmos efeitos sobre logons (conexões de modelo tradicional) e usuários de bancos de dados independentes. Para obter mais informações sobre o firewall do Windows, veja [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
### <a name="sssds-firewalls"></a>[!INCLUDE[ssSDS](../../includes/sssds-md.md)] Firewalls  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] permite regras de firewall separadas para conexões (logons) em nível de servidor e para conexões de nível de banco de dados (usuários de bancos de dados independentes). Ao se conectar a um banco de dados do usuário, primeiramente as regras de firewall do banco de dados são verificadas. Se não houver nenhuma regra que permita o acesso ao banco de dados, as regras de firewall em nível de servidor serão verificadas, o que requer acesso ao banco de dados mestre do servidor lógico. Regras de firewall em nível de banco de dados combinadas a usuários de banco de dados independente podem eliminar a necessidade de acessar o banco de dados mestre do servidor durante a conexão, resultando assim em uma melhor escalabilidade de conexão.  
  
 Para obter mais informações sobre as regras de firewall do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , veja os seguintes tópicos:  
  
-   [Firewall do banco de dados SQL do Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx)  
  
-   [Como: definir as configurações do firewall (Banco de Dados SQL do Azure)](https://msdn.microsoft.com/library/azure/jj553530.aspx)  
  
-   [sp_set_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](/sql/relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database)  
  
-   [sp_set_database_firewall_rule &#40;Banco de Dados SQL do Azure&#41;](/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database)  
  
## <a name="syntax-differences"></a>Diferenças de sintaxe  
  
|Modelo tradicional|Modelo de usuário de banco de dados independente|  
|-----------------------|-----------------------------------|  
|Quando conectado ao banco de dados mestre:<br /><br /> `CREATE LOGIN login_name  WITH PASSWORD = 'strong_password';`<br /><br /> Em seguida, quando conectado a um banco de dados do usuário:<br /><br /> `CREATE USER 'user_name' FOR LOGIN 'login_name';`|Quando conectado a um banco de dados do usuário:<br /><br /> `CREATE USER user_name  WITH PASSWORD = 'strong_password';`|  
  
|Modelo tradicional|Modelo de usuário de banco de dados independente|  
|-----------------------|-----------------------------------|  
|Para alterar a senha no contexto do banco de dados mestre:<br /><br /> `ALTER LOGIN login_name  WITH PASSWORD = 'strong_password';`|Para alterar a senha no contexto do banco de dados do usuário:<br /><br /> `ALTER USER user_name  WITH PASSWORD = 'strong_password';`|  
  
## <a name="remarks"></a>Comentários  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], usuários de bancos de dados independentes devem estar habilitados para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Opção contained database authentication de configuração de servidor](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md).  
  
-   Os usuários do banco de dados independente e logons com nomes não sobrepostas podem coexistir em seus aplicativos.  
  
-   Se houver um logon no banco de dados mestre com nome **name1** e você criar um usuário de banco de dados independente denominado **name1**, quando um nome de banco de dados for fornecido para a cadeia de conexão, o contexto do usuário de banco de dados será escolhido de acordo com o contexto de logon ao se conectar ao banco de dados. Ou seja, os usuários do banco de dados independente têm precedência sobre logons com o mesmo nome.  
  
-   No [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , o nome de usuário de banco de dados independente não pode ser igual ao nome da conta de administrador de servidor.  
  
-   A conta de administrador do servidor [!INCLUDE[ssSDS](../../includes/sssds-md.md)] nunca pode ser um usuário de banco de dados independente. O administrador do servidor tem permissões suficientes para criar e gerenciar usuários de banco de dados independente. O administrador do servidor pode conceder permissões a usuários de banco de dados independente em bancos de dados do usuário.  
  
-   Uma vez que os usuários de banco de dados independente são entidades de nível de banco de dados, você precisa criar usuários de banco de dados independente em todos os bancos de dados em que eles forem ser usados. A identidade está restrita ao banco de dados e é independente, em todos os aspectos, de um usuário com o mesmo nome e a mesma senha em outro banco de dados, no mesmo servidor.  
  
-   Use senhas com a mesma força que normalmente usaria para logons.  
  
## <a name="see-also"></a>Consulte Também  
 [Bancos de dados independentes](../databases/contained-databases.md)   
 [Práticas recomendadas de segurança com bancos de dados independentes](../databases/security-best-practices-with-contained-databases.md)   
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
  
