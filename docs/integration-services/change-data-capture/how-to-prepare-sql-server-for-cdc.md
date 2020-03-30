---
title: Como preparar o SQL Server para CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f13e8eae235eb040e92baa15247b6094e9aa1075
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294696"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>Como Preparar o SQL Server para CDC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O serviço Oracle CDC exige que todas as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino contenham o banco de dados MSXDBCDC. Você cria este banco de dados usando a ação Preparar SQL Server no Console de Configuração do Serviço CDC. Esta tarefa é feita uma vez somente para cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 Veja a seguir uma descrição sobre como preparar um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para Change Data Capture da Oracle usando o Console de Configuração do Serviço CDC. Este processo cria o banco de dados MSXDBCDC e define as tabelas necessárias, os procedimentos armazenados e outros artefatos necessários.  
  
 A preparação do SQL Server para Oracle CDC é feito pelo Administrador de Serviço Oracle CDC. Para obter mais informações sobre a função de Administrador de Serviço CDC, consulte [User Roles](../../integration-services/change-data-capture/user-roles.md).  
  
### <a name="to-enable-sql-server-for-cdc"></a>Para habilitar o SQL Server para CDC  
  
1.  No menu **Iniciar** , selecione **Configuração do Serviço CDC para Oracle**.  
  
2.  No painel esquerdo, selecione **Serviços Locais CDC** no painel **Ações** e clique em **Preparar SQL Server**.  
  
     Você também pode clicar com o botão direito do mouse em **Local CDC Services (Serviços Locais de CDC)** e selecionar **Prepare SQL Server (Preparar SQL Server)** .  
  
3.  Insira as informações necessárias na caixa de diálogo Preparando a Instância SQL Server para Oracle CDC. Para obter informações sobre como inserir as informações necessárias nessa caixa de diálogo, consulte [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md).  
  
     Para Preparar a instância do SQL Server para Oracle CDC, o logon deve ter permissão de gravação no banco de dados MSXDBCDC. Insira as credenciais para um logon que tem permissão de gravação no banco de dados MSXDBCDC, como um membro da função `sysasmin` .  
  
 **Observação**: clique em **Exibir Script** para exibir uma versão somente leitura do script de instalação. Um administrador do sistema do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode copiar este script no Console de Gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para editá-lo e executá-lo, se for necessário.  
  
## <a name="see-also"></a>Consulte Também  
 [Preparar o SQL Server para CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
