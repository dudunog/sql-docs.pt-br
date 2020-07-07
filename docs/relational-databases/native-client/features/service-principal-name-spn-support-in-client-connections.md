---
title: Nome da entidade de serviço em conexões
description: Saiba mais sobre o suporte para nomes de entidade de serviço para autenticação mútua no SQL Server Native Client.
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, SPNs
- ODBC, SPNs
- OLE DB, SPNs
- SPNs [SQL Server]
ms.assetid: 96598c69-ce9a-4090-aacb-d546591e8af7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6dcafb11041fc3698e0af5db31d05e95263dd268
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86009014"
---
# <a name="service-principal-name-spn-support-in-client-connections"></a>Suporte a SPN (Nome da entidade de serviço) em conexões com o cliente
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] em diante, o suporte para SPNs (nomes das entidades de serviço) foi estendido para habilitar a autenticação mútua em todos os protocolos. Em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], apenas havia suporte para SPNs no Kerberos via TCP quando o SPN padrão da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] era registrado no Active Directory.  
  
 Os SPNs são usados pelo protocolo de autenticação para determinar a conta na qual uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é executada. Se a conta da instância for conhecida, autenticação Kerberos poderá ser usada para fornecer autenticação mútua pelo cliente e servidor. Se a conta de instância não for conhecida, a autenticação NTLM, que só fornece autenticação do cliente pelo servidor, será usada. Atualmente, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client executa a pesquisa de autenticação, derivando o SPN das propriedades de nome da instância e conexão de rede. As instâncias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tentarão registrar os SPNs na inicialização, ou eles podem ser registrados manualmente. Porém, o registro falhará se houver direitos de acesso insuficientes para a conta que tenta registrar os SPNs.  
  
 As contas de domínio e computador são registradas automaticamente no Active Directory. Elas podem ser usadas como SPNs ou os administradores podem definir seus próprios SPNs. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] torna a autenticação segura mais gerenciável e confiável, permitindo que os clientes especifiquem diretamente o SPN a ser usado.  
  
> [!NOTE]  
>  Um SPN especificado por um aplicativo cliente é usado somente quando uma conexão é feita com a segurança integrada pelo Windows.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Kerberos Configuration Manager for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** é uma ferramenta de diagnóstico que ajuda a solucionar problemas de Kerberos relativos à conectividade com [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
 Para obter mais informações sobre Kerberos, consulte os artigos a seguir:  
  
-   [Suplemento técnico do Kerberos para Windows](/previous-versions/msp-n-p/ff649429(v=pandp.10))  
  
-   [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)  
  
## <a name="usage"></a>Uso  
 A tabela a seguir descreve os cenários mais comuns nos quais os aplicativos cliente podem habilitar a autenticação segura.  
  
|Cenário|DESCRIÇÃO|  
|--------------|-----------------|  
|Um aplicativo herdado não especifica um SPN.|Este cenário de compatibilidade garante que não haverá nenhuma alteração de comportamento para aplicativos desenvolvidos para versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se nenhum SPN for especificado, o aplicativo confiará nos SPNs gerados e não terá nenhum conhecimento de qual método de autenticação será usado.|  
|Um aplicativo cliente que usa a versão anterior do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client especifica um SPN na cadeia de conexão como um usuário do domínio ou uma conta de computador, como um SPN específico da instância ou uma cadeia definida pelo usuário.|A palavra-chave **ServerSPN** pode ser usada em um provedor, uma inicialização ou uma cadeia de conexão para fazer o seguinte:<br /><br /> – Especificar a conta usada pela instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para uma conexão. Isto simplifica o acesso à autenticação Kerberos. Se um KDC (Centro de Distribuição de Chaves) Kerberos estiver presente e a conta correta for especificada, a autenticação Kerberos provavelmente será mais usada que NTLM. O KDC normalmente reside no mesmo computador que o controlador de domínio.<br /><br /> – Especificar um SPN para pesquisar a conta de serviço para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para cada instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], são gerados dois SPNs padrão que podem ser usados para essa finalidade. Não há garantia de que estas chaves estejam presentes no Active Directory. Entretanto, nesta situação, a autenticação Kerberos não é garantida.<br /><br /> – Especificar um SPN que será usado para pesquisar a conta de serviço para a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Esta poderá ser qualquer cadeia de caracteres definida pelo usuário que mapeia para a conta de serviço. Neste caso, a chave deve ser registrada manualmente no KDC e deve satisfazer as regras para um SPN definido pelo usuário.<br /><br /> A palavra-chave **FailoverPartnerSPN** pode ser usada para especificar o SPN para o servidor de parceiro de failover. O intervalo de conta e valores de chave do Active Directory é igual aos valores que você pode especificar para o servidor principal.|  
|Um aplicativo ODBC especifica um SPN como um atributo de conexão para o servidor principal ou servidor de parceiro de failover.|O atributo de conexão **SQL_COPT_SS_SERVER_SPN** pode ser usado para especificar o SPN para uma conexão com o servidor principal.<br /><br /> O atributo de conexão **SQL_COPT_SS_FAILOVER_PARTNER_SPN** pode ser usado para especificar o SPN para o servidor de parceiro de failover.|  
|Um aplicativo OLE DB especifica um SPN como uma propriedade de inicialização de fonte de dados para o servidor principal ou para um servidor de parceiro de failover.|A propriedade de conexão **SSPROP_INIT_SERVER_SPN** no conjunto de propriedades **DBPROPSET_SQLSERVERDBINIT** pode ser usada para especificar o SPN para uma conexão.<br /><br /> A propriedade de conexão **SSPROP_INIT_FAILOVER_PARTNER_SPN** na **DBPROPSET_SQLSERVERDBINIT** pode ser usada para especificar o SPN para o servidor de parceiro de failover.|  
|Um usuário especifica um SPN para um servidor ou servidor de parceiro de failover em um DSN (nome de fonte de dados) ODBC.|O SPN pode ser especificado em um DSN ODBC pelas caixas de diálogo de configuração do DSN.|  
|O usuário especifica um SPN para um servidor ou servidor de parceiro de failover em uma caixa de diálogo **Vínculo de Dados** ou **Logon** no OLE DB.|O SPN pode ser especificado em uma caixa de diálogo **Vínculo de Dados** ou **Logon** . A caixa de diálogo **Logon** pode ser usada com ODBC ou OLE DB.|  
|Um aplicativo ODBC determina o método de autenticação usado para estabelecer uma conexão.|Quando uma conexão foi aberta com êxito, um aplicativo pode consultar o atributo de conexão **SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD** para determinar qual método de autenticação foi usado. Os valores incluirão (mas não estarão limitados a) **NTLM** e **Kerberos**.|  
|Um aplicativo OLE DB determina o método de autenticação usado para estabelecer uma conexão.|Quando uma conexão foi aberta com êxito, um aplicativo pode consultar a propriedade de conexão **SSPROP_AUTHENTICATION_METHOD** no conjunto de propriedades **DBPROPSET_SQLSERVERDATASOURCEINFO** para determinar qual método de autenticação foi usado. Os valores incluirão (mas não estarão limitados a) **NTLM** e **Kerberos**.|  
  
## <a name="failover"></a>Failover  
 Os SPNs não são armazenados no cache de failover e, portanto, não podem ser transmitidos entre conexões. Os SPNs serão usados em todas as tentativas de conexão com a entidade e o parceiro quando especificados na cadeia de conexão ou nos atributos de conexão.  
  
## <a name="connection-pooling"></a>Pool de conexões  
 Os aplicativos devem estar atentos que especificar SPNs em algumas, mas não em todas as cadeias de conexão, podem contribuir para o agrupamento da fragmentação.  
  
 Os aplicativos podem especificar SPNs programaticamente como atributos de conexão, em vez de especificar palavras-chave da cadeia de conexão. Isto pode ajudar no gerenciamento da fragmentação do pool de conexões.  
  
 Os aplicativos deverão saber que os SPNs nas cadeias de conexão possam ser substituídos definindo os atributos de conexão correspondentes, mas as cadeias de conexão usadas pelo pool de conexões usarão os valores da cadeia de conexão para fins de pool.  
  
## <a name="down-level-server-behavior"></a>Comportamento de servidor de versão anterior  
 O novo comportamento de conexão é implementado pelo cliente; portanto, ele não é específico para uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="linked-servers-and-delegation"></a>Servidores vinculados e delegação  
 Quando servidores vinculados são criados, o parâmetro ** \@ parâmetro provstr** de [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) pode ser usado para especificar os SPNs do servidor e do parceiro de failover. Os benefícios disso é o mesmo que especificar SPNs em cadeias de conexão de cliente. É mais simples e confiável estabelecer conexões que usam autenticação Kerberos.  
  
 A delegação com servidores vinculados exige a autenticação Kerberos.  
  
## <a name="management-aspects-of-spns-specified-by-applications"></a>Aspectos de gerenciamento de SPNs especificados por aplicativos  
 Ao escolher se deseja especificar SPNs em um aplicativo (por meio de cadeias de conexão) ou, programaticamente, por meio de propriedades de conexão (em vez de confiar no provedor padrão gerado por SPNs), considere os seguintes fatores:  
  
-   Segurança: o SPN especificado divulga informações que estão protegidas?  
  
-   Confiabilidade: para permitir o uso de SPNs padrão, a conta de serviço na qual a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é executada precisa ter privilégios suficientes para atualizar o Active Directory no KDC.  
  
-   Conveniência e transparência de local: como os SPNs de um aplicativo serão afetados se seu banco de dados for movido para uma instância diferente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ? Isto se aplicará ao servidor principal e seu parceiro de failover se você usar espelhamento de banco de dados. Se uma alteração de servidor significar que os SPNs devem ser alterados, como isto afetará os aplicativos? Qualquer alteração será gerenciada?  
  
## <a name="specifying-the-spn"></a>Especificando o SPN  
 Você pode especificar um SPN em caixas de diálogo e em código. Esta seção discute como você pode especificar um SPN.  
  
 O tamanho máximo de um SPN é 260 caracteres.  
  
 A sintaxe que os SPNs usam em cadeia de conexão ou atributos de conexão é a seguinte:  
  
|Sintaxe|Descrição|  
|------------|-----------------|  
|MSSQLSvc/*FQDN*|O SPN padrão gerado pelo provedor para uma instância padrão quando um protocolo diferente de TCP é usado.<br /><br /> *FQDN* é um nome de domínio totalmente qualificado.|  
|MSSQLSvc/*fqdn*:*port*|O SPN padrão gerado pelo provedor quando o protocolo TCP é usado.<br /><br /> *port* é um número de porta TCP.|  
|MSSQLSvc/*FQDN*:*InstanceName*|O SPN padrão gerado pelo provedor para uma instância nomeada quando um protocolo diferente de TCP é usado.<br /><br /> *InstanceName* é um nome de instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|HOST/*fqdn*<br /><br /> HOST/*MachineName*|O SPN que mapeia para contas internas do computador que são automaticamente registradas pelo Windows.|  
|*Nome de usuário* @ *Domínio* do|Especificação direta de uma conta de domínio.<br /><br /> *Username* é um nome de conta de usuário do Windows.<br /><br /> *Domain* é um nome de domínio ou nome de domínio totalmente qualificado do Windows.|  
|*MachineName* $@ *Domínio* do|Especificação direta de uma conta de computador.<br /><br /> (Se o servidor ao qual você está se conectando estiver sendo executado em contas LOCAL SYSTEM ou NETWORK SERVICE, para obter autenticação Kerberos, o **ServerSPN** poderá estar no formato *MachineName*$@*Domain* .)|  
|*KDCKey* / *MachineName*|Um SPN especificado pelo usuário.<br /><br /> *KDCKey* é uma cadeia de caracteres alfanumérica que está em conformidade com as regras para uma chave do KDC.|  
  
## <a name="odbc-and-ole-db-syntax-supporting-spns"></a>Sintaxe do ODBC e OLE DB que dão suporte a SPNs  
 Para informações específicas de sintaxe, consulte os seguintes tópicos:  
  
-   [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [SPNs &#40;Nomes da Entidade de Serviço&#41; em conexões de cliente &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
 Para obter informações sobre aplicativos de exemplo que demonstram esse recurso, consulte [Exemplos de programabilidade de dados do SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
[Registrar um nome de entidade de serviço para conexões de Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
