---
title: Configurar permissões do sistema de arquivos para acesso ao Mecanismo de Banco de Dados | Microsoft Docs
description: Saiba mais sobre os SIDs por serviço. Confira como conceder permissão de acesso à localização do arquivo de banco de dados para que o Mecanismo de Banco de Dados possa acessar os arquivos de banco de dados.
ms.custom: ''
ms.date: 06/06/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- file system permissions
- service account [SQL Server], file system permissions
- permissions [SQL Server], file system
ms.assetid: 78bba43c-4edb-4216-84ac-d6246ae5546d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 69eca7c64ddf6f48057b8b1f5fafa34f02434355
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637755"
---
# <a name="configure-file-system-permissions-for-database-engine-access"></a>Configurar permissões do sistema de arquivos para acesso ao mecanismo de banco de dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como conceder ao [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]acesso ao sistema de arquivos ao local onde os arquivos de banco de dados são armazenados. O serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve ter a permissão do sistema de arquivos do Windows para acessar a pasta onde os arquivos de banco de dados são armazenados. A permissão para o local padrão é configurada durante a instalação. Se você colocar seus arquivos de banco de dados em um local diferente, poderá precisar seguir estas etapas para conceder ao [!INCLUDE[ssDE](../../includes/ssde-md.md)] a permissão de controle total para esse local.  
  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , as permissões são atribuídas ao SID por serviço para cada um de seus serviços. Este sistema ajuda a fornecer o isolamento de serviço e defesa mais eficiente. O SID por serviço é derivado do nome do serviço e é exclusivo a cada serviço. O tópico [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md) descreve o SID por serviço e fornece os nomes na seção **Privilégios e direitos do Windows**. É o SID por serviço que deve receber a permissão de acesso no local do arquivo.  
  
## <a name="to-grant-file-system-permission-to-the-per-service-sid"></a>Para conceder permissão do sistema de arquivos ao SID por serviço  
  
1.  Usando o Windows Explorer, navegue até o local do sistema de arquivos onde os arquivos de banco de dados são armazenados. Clique com o botão direito do mouse na pasta do sistema de arquivos e clique em **Propriedades**.  
  
2.  Na guia **Segurança** , clique em **Editar**e em **Adicionar**.  
  
3.  Na caixa de diálogo **Selecionar Usuários, Computadores, Conta de Serviço ou Grupos** , clique em **Localizações**na parte superior da lista de localizações, selecione o nome de seu computador e clique em **OK**.  
  
4.  Na caixa **Inserir os nomes de objeto a serem selecionados** , digite o nome do SID por serviço listado no tópico [**Configurar contas de serviço e permissões do Windows**](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)dos Manuais Online. (Para o nome do SID por serviço do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , use **NT SERVICE\MSSQLSERVER** para uma instância padrão ou **NT SERVICE\MSSQL$NomeInstância** para uma instância nomeada.)  
  
5.  Clique em **Verificar Nomes** para validar a entrada. (Em caso de falha na validação, você poderá receber um alerta informando que o nome não foi encontrado. Quando você clica em **OK**, uma caixa de diálogo **Vários nomes encontrados** é exibida. Agora selecione o nome do SID por serviço, **MSSQLSERVER** ou **NT SERVICE\MSSQL$NomeInstância**e clique em **OK**.  Clique em **OK** novamente para retornar à caixa de diálogo **Permissões** .)   
6.  Na caixa de nomes de **Grupo ou usuário**, selecione o nome do SID por serviço e, na caixa **Permissões para** \<name>, marque a caixa de seleção **Permitir** para **Controle total**.  
  
7. Clique em **Aplicar**e em **OK** duas vezes para sair.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar os serviços do Mecanismo de Banco de Dados](../../database-engine/configure-windows/manage-the-database-engine-services.md)   
 [Mover bancos de dados do sistema](../../relational-databases/databases/move-system-databases.md)   
 [Mover bancos de dados de usuário](../../relational-databases/databases/move-user-databases.md)  
  
  
