---
title: Modificar contas de serviços de controlador e de cliente
titleSuffix: SQL Server Distributed Replay
description: Aprenda a modificar as contas dos serviços controlador e cliente do Distributed Replay e, em seguida, reaplicar as listas de controle de acesso.
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 44a73ddb-18ad-415c-bfbe-126ab2e3290b
author: MikeRayMSFT
ms.author: mikeray
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 7abe40c16dc49e948fbca68486f96db221e1aae8
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000394"
---
# <a name="modify-the-controller-and-client-services-accounts"></a>Modificar as contas de serviços de controlador e de cliente

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Neste tópico, você aprenderá a modificar o controlador Distributed Replay e as contas de serviço cliente e depois reaplicar as ACLs (listas de controle de acesso).  
  
### <a name="to-start-or-stop-the-distributed-replay-services-using-computer-management"></a>Para iniciar ou parar os serviços Distributed Replay usando o gerenciamento do computador  
  
1.  No computador em que os serviços Distributed Replay estão instalados, no prompt de comando, digite **dcomcnfg**.  
  
2.  Clique duas vezes em **Serviços**, role para baixo e clique com o botão direito do mouse em **<nome do serviço> do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay\<** e clique em **Iniciar** ou em **Parar**.  
  
### <a name="to-modify-the-distributed-replay-controller-service"></a>Para modificar o serviço controlador Distributed Replay  
  
1.  No computador controlador, pare o serviço controlador [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay.  
  
2.  Em **Serviços**, clique com o botão direito do mouse em **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay**e selecione **Propriedades**.  
  
3.  Na janela **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay** , na guia **Logon** , selecione **Esta conta**, digite ou clique em **Procurar** para inserir a nova conta de logon e clique em **OK**.  
  
     **Importante**: Ao configurar o Distributed Replay Controller é possível especificar uma ou mais contas de usuário que serão usadas para executar os serviços de cliente do Distributed Replay. Esta é a lista das contas com suporte:  
  
    -   Conta de usuário do domínio  
  
    -   Conta de usuário local criada pelo usuário  
  
    -   Administrador  
  
    -   Conta virtual e MSA (Conta de Serviço Gerenciada)  
  
    -   Serviços de rede, serviços locais e sistema  
  
     Não são aceitas contas de grupo (local ou domínio) e outras contas internas (como Todos).  
  
4.  Inicie o serviço controlador Distributed Replay.  
  
### <a name="to-modify-the-distributed-replay-client-service"></a>Para modificar o serviço cliente do Distributed Replay  
  
1.  Antes de modificar o serviço cliente Distributed Replay, verifique se a conta do serviço cliente que você está alterando foi especificada durante a configuração (no parâmetro CTLRUSERS no computador controlador). Se a conta de serviço de cliente que você está alterando não foi especificada durante a instalação, execute as etapas a seguir primeiro:  
  
    1.  Pare o serviço controlador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay.  
  
    2.  No computador controlador em que o serviço controlador está instalado, no prompt de comando, digite **dcomcnfg**.  
  
    3.  Na janela **Serviços de Componente**, navegue até **Raiz do Console -> Serviços de Componente -> Computadores -> Meu Computador -> Configuração de DCOM ->DReplayController**.  
  
    4.  Clique com o botão direito do mouse em **DReplayController**e clique em **Propriedades**.  
  
    5.  Na janela **Propriedades do DReplayController** , na guia **Segurança** , clique em **Editar** na seção **Permissões de Inicialização e Ativação** .  
  
    6.  Conceda à nova conta de logon do serviço cliente permissões de **Ativação Local e Remota** e clique em **OK**.  
  
    7.  Clique em **Editar** na seção **Permissões de Acesso** e conceda à nova conta de logon do serviço cliente permissões de **Acesso Local e Remoto** e clique em **OK**.  
  
    8.  Clique em **OK** para fechar a janela **Propriedades do DReplayController** .  
  
    9. No computador controlador, adicione a conta de logon do serviço cliente alterado para o grupo **Usuários COM Distribuídos** .  
  
    10. Inicie o serviço controlador SQL Server Distributed Replay.  
  
2.  Pare o serviço cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay.  
  
3.  Na janela **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay** , na guia **Logon** , selecione **Esta conta**, digite ou clique em **Procurar** para inserir a nova conta de logon e clique em **OK**.  
  
4.  Inicie o serviço cliente Distributed Replay.  
  
  
