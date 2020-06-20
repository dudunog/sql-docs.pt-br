---
title: Assistente para Criar Banco de Dados (Gerenciador de Configuração do Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.createdbwiz.f1
ms.assetid: 45fe7a23-a46c-4d40-8bca-3431fbfc5c9d
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 92de52229959559a03dac29e40035fbe4438ebc7
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971686"
---
# <a name="create-database-wizard-master-data-services-configuration-manager"></a>Assistente para Criar Banco de Dados (Gerenciador de Configuração do Master Data Services)
  Use o assistente para **Criar Banco de Dados** para criar um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
## <a name="database-server"></a>Servidor de Banco de Dados  
 Especifique as informações para conexão com uma instância local ou remota do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] na qual hospedar o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Para conexão com uma instância remota, o banco de dados deve estar habilitado para conexões remotas.  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Instância do SQL Server**|Especifique o nome da instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] na qual deseja hospedar o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Pode ser uma instância padrão ou nomeada em um computador local ou remoto. Especifique as informações digitando:<br /><br /> Um ponto (.) para se conectar à instância padrão no computador local.<br /><br /> O nome do servidor ou o endereço IP para conectar à instância padrão no computador local ou remoto especificado.<br /><br /> O nome do servidor ou o endereço IP e o nome da instância para conexão à instância nomeada no computador local ou remoto especificado. Especifique essas informações no formato *server_name* \\ *instance_name*.|  
|**Tipo de autenticação**|Selecione o tipo de autenticação a ser usado ao conectar à instância do SQL Server especificada. As credenciais usadas para conexão devem fazer parte da função de servidor **sysadmin** para a instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada. Para obter mais informações sobre a função sysadmin , veja [Funções de nível de servidor](../relational-databases/security/authentication-access/server-level-roles.md). Os tipos de autenticação incluem:<br /><br /> **Segurança integrada do usuário atual**: usa a autenticação integrada do Windows para se conectar usando as credenciais da conta de usuário do Windows atual. [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] usa as credenciais do Windows do usuário que fez logon no computador e abriu o aplicativo. Não é possível especificar credenciais diferentes do Windows no aplicativo. Para conectar-se com credenciais diferentes do Windows, faça logon no computador como esse usuário e abra o [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].<br /><br /> **Conta do SQL Server**: usa uma conta do SQL Server para a conexão. Quando você seleciona essa opção, os campos **Nome de usuário** e **Senha** são habilitados e você deve especificar credenciais de uma conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**Nome de usuário**|Especifique o nome da conta de usuário que será usada para conexão à instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . A conta deve fazer parte da função **sysadmin** na [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instância especificada.<br /><br /> Quando o **tipo de autenticação** é **segurança integrada ao usuário atual**, a caixa **nome de usuário** é somente leitura e exibe o nome da conta de usuário do Windows que está conectada ao computador.<br /><br /> Quando o **Tipo de autenticação** é **Conta do SQL Server**, a caixa **Nome de usuário** está habilitada e você deve especificar credenciais para uma conta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] na instância especificada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .|  
|**Senha**|Especifique a senha associada à conta de usuário.<br /><br /> Quando o **tipo de autenticação** é **segurança integrada ao usuário atual**, a caixa **senha** é somente leitura e as credenciais da conta de usuário do Windows especificada são usadas para se conectar.<br /><br /> Quando o **Tipo de autenticação** é **Conta do SQL Server**, a caixa **Senha** está habilitada e você deve especificar a senha associada à conta de usuário especificada.|  
|**Testar conexão**|Verifique se a conta de usuário especificada pode se conectar à instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e se a conta tem permissão para criar um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] nessa instância. Se você não clicar em **Testar Conexão**, a conexão será testada quando você clicar em **Avançar**.|  
  
## <a name="database"></a>Banco de dados  
 Especifique um nome de banco de dados e as opções de ordenação para o novo banco de dados. As ordenações em [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornecem propriedades de regras de classificação, de diferenciação de maiúsculas e minúsculas e de diferenciação de acentos para seus dados. As ordenações utilizadas com tipos de dados de caractere, como char e varchar, determinam a página de código e os caracteres correspondentes que podem ser representados para o tipo de dados em questão. Para obter mais informações sobre ordenação de banco de dados, consulte [Suporte a ordenações e a Unicode](../relational-databases/collations/collation-and-unicode-support.md).  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Nome do banco de dados**|Especifique um nome para o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .|  
|**Ordenação padrão do SQL Server**|Selecione para usar a configuração de ordenação atual do banco de dados da instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificada para o novo banco de dados.|  
|**Ordenação do Windows**|Especifique as configurações de ordenação do Windows para uso com o novo banco de dados. As ordenações do Windows definem regras para armazenar dados de caractere com base em uma localidade do Windows associada. Para obter mais informações sobre ordenações do Windows e as opções associadas, consulte [Nome de ordenação do Windows &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql).<br /><br /> Observação: a lista **Ordenação do Windows** e as opções associadas são habilitadas apenas depois de você desmarcar a caixa **Ordenação padrão do SQL Server**.|  
  
## <a name="administrator-account"></a>Conta Administrador  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Nome de usuário**|Especifique uma conta de usuário de domínio para ser o administrador do sistema do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]. Para todos os [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] aplicativos da Web associados a esse banco de dados, esse usuário pode atualizar todos os modelos e todos eles em todas as áreas funcionais. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](administrators-master-data-services.md).|  
  
## <a name="summary"></a>Resumo  
 Exibe um resumo das opções selecionadas. Examine suas seleções e clique em **Avançar** para começar a criar o banco de dados com as configurações especificadas.  
  
## <a name="progress-and-finish"></a>Progresso e Conclusão  
 Exibe o progresso do processo de criação. Depois que o banco de dados for criado, clique em **Concluir** para fechar o assistente de banco de dados e retornar à página **Bancos de dados** . O novo banco de dados é selecionado e você pode exibir e modificar as configurações do sistema.  
  
## <a name="see-also"></a>Consulte Também  
 [Página de configuração do banco de dados &#40;Gerenciador de Configuração do Master Data Services&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Configurar o banco de dados e o site para Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Requisitos do banco de dados &#40;Master Data Services&#41;](install-windows/database-requirements-master-data-services.md)  
  
  
