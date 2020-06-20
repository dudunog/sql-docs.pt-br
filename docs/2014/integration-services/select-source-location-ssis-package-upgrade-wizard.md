---
title: Selecionar local de origem (Assistente de atualização de pacotes SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.is.upgradewizard.selectsourcelocation.f1
ms.assetid: 429f146e-edb4-4401-a225-f2c8468971c5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 90cb7110a6b4e9372fe5397ba050f91535a58f94
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84963666"
---
# <a name="select-source-location-ssis-package-upgrade-wizard"></a>Selecionar Local de Origem (Assistente de Atualização de Pacotes SSIS)
  Use a página **Selecionar Local de Origem** para especificar a origem a partir da qual os pacotes serão atualizados.  
  
> [!NOTE]  
>  Essa página só está disponível quando o Assistente de Atualização de Pacotes do [!INCLUDE[ssIS](../includes/ssis-md.md)] é executado por meio do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou no prompt de comando.  
  
 **Para executar o Assistente de Atualização de Pacotes SSIS**  
  
-   [Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS](install-windows/upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md)  
  
## <a name="static-options"></a>Opções estáticas  
 **Origem do pacote**  
 Selecione o local de armazenamento que contém os pacotes a serem atualizados. Os valores dessa opção estão relacionados na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Sistema de Arquivos**|Indica que os pacotes a serem atualizados estão em uma pasta no computador local.<br /><br /> Para que o assistente faça backup dos pacotes originais antes de atualizá-los, esses pacotes devem ser armazenados no sistema de arquivos. Para obter mais informações, consulte o tópico de instruções.|  
|**Armazenamento de Pacotes SSIS**|Indica que os pacotes a serem atualizados estão no armazenamento de pacotes. O repositório de pacotes consiste no conjunto de pastas do sistema de arquivos gerenciado pelo serviço do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](service/package-management-ssis-service.md).<br /><br /> Selecione esse valor para exibir as opções dinâmicas de **Origem do pacote** correspondentes.|  
|**Microsoft SQL Server**|Indica que os pacotes a serem atualizados são de uma instância existente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Selecione esse valor para exibir as opções dinâmicas de **Origem do pacote** correspondentes.|  
  
 **Pasta**  
 Digite o nome de uma pasta que contém os pacotes que você quer atualizar ou clique em **Procurar** e localize a pasta.  
  
 **Procurar**  
 Navegue para localizar a pasta que contém os pacotes você deseja atualizar.  
  
## <a name="package-source-dynamic-options"></a>Opções dinâmicas de Origem do pacote  
  
### <a name="package-source--ssis-package-store"></a>Origem do pacote = Repositório de Pacotes SSIS  
 **Servidor**  
 Digite o nome do servidor que tem os pacotes a serem atualizados ou selecione esse servidor na lista.  
  
### <a name="package-source--microsoft-sql-server"></a>Origem do pacote = Microsoft SQL Server  
 **Servidor**  
 Digite o nome do servidor que tem os pacotes a serem atualizados ou selecione esse servidor na lista.  
  
 **Usar autenticação do Windows**  
 Selecione para usar a Autenticação do Windows para estabelecer conexão com o servidor.  
  
 **Usar Autenticação do SQL Server**  
 Selecione para usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para estabelecer conexão com o servidor. Se você usar a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , será preciso fornecer um nome de usuário e uma senha.  
  
 **Nome de usuário**  
 Digite o nome de usuário que a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará para estabelecer conexão com o servidor.  
  
 **Senha**  
 Digite a senha que a Autenticação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usará para estabelecer conexão com o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizar pacotes do Integration Services](install-windows/upgrade-integration-services-packages.md)  
  
  
