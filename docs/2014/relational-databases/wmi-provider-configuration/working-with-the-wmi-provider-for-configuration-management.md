---
title: Trabalhando com o provedor WMI para o gerenciamento de configuração | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b4a4c956f1bf60f6d874ee2bda3b261dd954836d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048863"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>Trabalhando com o provedor WMI para o Gerenciamento de configuração
  Considere o seguinte antes de programar com o provedor WMI para Gerenciamento do Computador:  
  
## <a name="binding"></a>Associação  
 O provedor WMI para gerenciamento de configuração é um modelo de objeto COM que dá suporte a associações iniciais e tardias. Com a associação tardia, você pode usar linguagens de script, como o VBScript, para manipular, de forma programada, os serviços, as configurações de rede e os aliases do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações sobre como programar implementações de provedor WMI usando linguagens de script, consulte o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [site](https://go.microsoft.com/fwlink/?linkid=15426)do MSDN.  
  
## <a name="specifying-a-connection-string"></a>Especificando uma cadeia de caracteres de conexão  
 Os aplicativos direcionam o provedor WMI para gerenciamento de configuração para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectando a um namespace WMI definido pelo provedor. O serviço Windows WMI mapeia esse namespace para a DLL do provedor e o carrega na memória. Todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são representadas com um único namespace WMI. O namespace assume este padrão  
  
```  
\\.\root\Microsoft\SqlServer\ComputerManagement12\instance_name  
```  
  
 onde `instance_name` assume `MSSQLSERVER` como padrão em uma instalação padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Observação:** Se você estiver se conectando por meio do firewall do Windows, precisará verificar se os computadores estão configurados corretamente. Consulte o artigo "conectando por meio do firewall do Windows" na documentação do Instrumentação de Gerenciamento do Windows no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [site](https://go.microsoft.com/fwlink/?linkid=15426)do MSDN.  
  
## <a name="permissions-and-server-authentication"></a>Permissões e autenticação do servidor  
 Para acessar o provedor WMI para gerenciamento de configuração, o script de gerenciamento WMI do cliente deve estar sendo executado no contexto de um administrador no computador de destino. Você precisa ser membro do grupo local de administradores do Windows no computador que deseja gerenciar.  
  
 O administrador pode definir políticas de grupo para controlar o acesso de usuários aos provedores WMI. Para obter mais informações sobre como definir políticas de grupo, consulte "Group Policy and MMC" na ajuda do Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 O script de gerenciamento WMI pode ser usado para atualizar a conta na qual os serviços do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são executados.  
  
 Os certificados de segurança são suportados pelo provedor WMI para gerenciamento de configuração. Para obter mais informações sobre certificados, consulte [hierarquia de criptografia](../security/encryption/encryption-hierarchy.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)  
  
  
