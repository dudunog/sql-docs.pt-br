---
description: sp_set_database_firewall_rule (Banco de Dados SQL do Azure)
title: sp_set_database_firewall_rule
titleSuffix: Azure SQL Database
ms.date: 08/04/2017
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_set_database_firewall_rule
- sp_set_database_firewall_rule_TSQL
- sys.sp_set_database_firewall_rule
- sys.sp_set_database_firewall_rule_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_set_database_firewall_rule
- firewall_rules, setting database rules
ms.assetid: 8f0506b6-a4ac-4e4d-91db-8077c40cb17a
author: VanMSFT
ms.author: vanto
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: b43c386f803c1d9fea8a1e7645d1764ece3a7eef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88493029"
---
# <a name="sp_set_database_firewall_rule-azure-sql-database"></a>sp_set_database_firewall_rule (Banco de Dados SQL do Azure)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Cria ou atualiza as regras de firewall no nível de banco de dados para seu [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] . As regras de firewall de banco de dados podem ser configuradas para o banco de dados **mestre** e para bancos de dados de usuário no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] . As regras de firewall de banco de dados são particularmente úteis ao usar usuários de banco de dados independente. Para obter mais informações, consulte [Usuários de bancos de dados independentes – Tornando seu banco de dados portátil](../../relational-databases/security/contained-database-users-making-your-database-portable.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_set_database_firewall_rule [@name = ] [N]'name'  
, [@start_ip_address =] 'start_ip_address'  
, [@end_ip_address =] 'end_ip_address'
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] [N]'name'` O nome usado para descrever e distinguir a configuração de firewall no nível de banco de dados. *nome* é **nvarchar (128)** sem valor padrão. O identificador Unicode `N` é opcional para [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] . 
  
`[ @start_ip_address = ] 'start_ip_address'` O endereço IP mais baixo no intervalo da configuração de firewall no nível de banco de dados. Os endereços IP iguais a ou maiores que esse podem tentar se conectar à instância do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais baixo possível é `0.0.0.0`. *start_ip_address* é **varchar (50)** sem valor padrão.  
  
`[ @end_ip_address = ] 'end_ip_address'` O endereço IP mais alto no intervalo da configuração de firewall no nível de banco de dados. Os endereços IP iguais a ou menores que esse podem tentar se conectar à instância do [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. O endereço IP mais alto possível é `255.255.255.255`. *end_ip_address* é **varchar (50)** sem valor padrão.  
  
 A tabela a seguir demonstra os argumentos e as opções com suporte no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] .  
  
> [!NOTE]  
>  As tentativas de conexão do Azure são permitidas quando esse campo e o campo de *start_ip_address* é igual a `0.0.0.0` .  
  
## <a name="remarks"></a>Comentários  
 Os nomes das configurações de firewall de nível de banco de dados para um banco de dados devem ser exclusivos. Se o nome da configuração do firewall em nível de banco de dados fornecida para o procedimento armazenado já existir na tabela de configurações de firewall de nível de banco de dados, os endereços IP inicial e final serão atualizados. Caso contrário, uma nova configuração de firewall de nível de banco de dados será criada.  
  
 Quando você adiciona uma configuração de firewall no nível de banco de dados em que os endereços IP inicial e final são iguais `0.0.0.0` , você habilita o acesso ao seu banco de dados no [!INCLUDE[ssSDS](../../includes/sssds-md.md)] servidor de qualquer recurso do Azure. Forneça um valor para o parâmetro *Name* que ajudará você a se lembrar do que é a configuração de firewall.  
  
## <a name="permissions"></a>Permissões  
 Exige a permissão **CONTROL** no banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O código a seguir cria uma configuração de firewall no nível de banco de dados chamada `Allow Azure` que habilita o acesso ao seu banco de dados a partir do Azure.  
  
```  
-- Enable Azure connections.  
EXECUTE sp_set_database_firewall_rule N'Allow Azure', '0.0.0.0', '0.0.0.0';  
  
```  
  
 O código a seguir cria uma configuração de firewall de nível de banco de dados chamada `Example DB Setting 1` somente para o endereço IP `0.0.0.4`. Em seguida, o `sp_set_database firewall_rule` procedimento armazenado é chamado novamente para atualizar o endereço IP final para `0.0.0.6` , nessa configuração de firewall. Isso cria um intervalo que permite endereços IP `0.0.0.4` , `0.0.0.5` e `0.0.0.6` para acessar o banco de dados.
  
```  
-- Create database-level firewall setting for only IP 0.0.0.4  
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.4';  
  
-- Update database-level firewall setting to create a range of allowed IP addresses
EXECUTE sp_set_database_firewall_rule N'Example DB Setting 1', '0.0.0.4', '0.0.0.6';  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Firewall do banco de dados SQL do Azure](https://azure.microsoft.com/documentation/articles/sql-database-firewall-configure/)   
 [Como: definir configurações de firewall (banco de dados SQL do Azure)](https://azure.microsoft.com/documentation/articles/sql-database-configure-firewall-settings/)   
 [sp_set_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-set-firewall-rule-azure-sql-database.md)   
 [sp_delete_database_firewall_rule &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-stored-procedures/sp-delete-database-firewall-rule-azure-sql-database.md)   
 [sys. database_firewall_rules &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-catalog-views/sys-database-firewall-rules-azure-sql-database.md)  
  
  
