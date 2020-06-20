---
title: Protocolos de rede e bibliotecas de rede | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- protocols [SQL Server]
- configuration options [SQL Server], protocols
- network libraries [SQL Server]
- protocols [SQL Server], about network protocols
- pipes [SQL Server]
- network protocols [SQL Server]
- default SQL Server configurations
- library [SQL Server]
- network protocols [SQL Server], about network protocols
- configuration options [SQL Server], libraries
ms.assetid: 8cd437f6-9af1-44ce-9cb0-4d10c83da9ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8be012ea2bc9499a99ca7763446c6f26cf219a18
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012218"
---
# <a name="network-protocols-and-network-libraries"></a>Protocolos de rede e bibliotecas de rede
  Um servidor pode escutar ou monitorar vários protocolos de rede ao mesmo tempo. Entretanto, cada protocolo deve ser configurado. Se um protocolo específico não for configurado, o servidor não poderá escutar naquele protocolo. Após a instalação, você pode alterar as configurações de protocolo usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
## <a name="default-sql-server-network-configuration"></a>Configuração de rede padrão do SQL Server  
 Uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurada para a porta TCP/IP 1433 e para o pipe nomeado \\\\.\pipe\sql\query. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são configuradas para portas dinâmicas TCP, com um número de porta atribuído pelo sistema operacional.  
  
 Se não for possível usar endereços de porta dinâmicos (por exemplo, quando as conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisam passar por um servidor de firewall configurado para passar por endereços de porta específicos). Selecione um número de porta não atribuído. As atribuições de número da porta são gerenciadas pela Internet Assigned Numbers Authority e são listadas em [http://www.iana.org](https://go.microsoft.com/fwlink/?LinkId=48844).  
  
 Para aumentar a segurança, a conectividade de rede não é habilitada completamente quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é instalado. Para habilitar, desabilitar e configurar protocolos de rede depois que a Instalação for concluída, use a Área de Configuração de Rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
## <a name="server-message-block-protocol"></a>Protocolo SMB  
 Os servidores na rede de perímetro devem ter todos os protocolos desnecessários desabilitados, incluindo o SMB. Os servidores Web e DNS (Sistema de Nome de Domínio) não requerem SMB. Este protocolo deve ser desabilitado para contra-atacar a ameaça de enumeração de usuário.  
  
> [!WARNING]
>  A desabilitação do protocolo SMB impede que o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou Cluster do Windows acesse o compartilhamento de arquivos remoto. Não desabilite o SMB se você implementa ou planeja implementar uma destas ações:  
> 
>  -   Usar o modo de quorum da maioria do compartilhamento de arquivos e o nó de Custer do Windows  
> -   Especificar um compartilhamento de arquivos SMB como o diretório de dados durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
> -   Criar um arquivo de banco de dados em um compartilhamento de arquivos SMB  
  
#### <a name="to-disable-smb"></a>Para desabilitar o SMB  
  
1.  No menu **Iniciar** , aponte para **Configurações**e clique em **Conexões Discadas e de Rede**.  
  
     Clique com o botão direito do mouse na conexão com a Internet e clique em **Propriedades**.  
  
2.  Marque a caixa de seleção **Cliente para Redes Microsoft** e clique em **Desinstalar**.  
  
3.  Siga as etapas de desinstalação.  
  
4.  Selecione **Compartilhamento arquivos/impressoras p/ redes Microsoft**e clique em **Desinstalar**.  
  
5.  Siga as etapas de desinstalação.  
  
#### <a name="to-disable-smb-on-servers-accessible-from-the-internet"></a>Para desabilitar o SMB em servidores acessíveis pela Internet  
  
-   Nas propriedades da Conexão Local, use a caixa de diálogo **Transmission Control Protocol/Internet Protocol (TCP/IP) properties (Propriedades de protocolo TCP/IP)** para remover **Compartilhamento arquivos/impressoras p/ redes Microsoft** e **Cliente para Redes Microsoft**.  
  
## <a name="endpoints"></a>Pontos de extremidade  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apresenta um novo conceito para conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ; a conexão é representada na extremidade do servidor por um [!INCLUDE[tsql](../../includes/tsql-md.md)]*ponto de extremidade*. As permissões podem ser concedidas, revogadas e negadas para pontos de extremidade [!INCLUDE[tsql](../../includes/tsql-md.md)] . Por padrão, todos os usuários têm permissões para acessar um ponto de extremidade, a menos que as permissões sejam negadas ou revogadas por um membro do grupo sysadmin ou pelo proprietário do ponto de extremidade. A sintaxe de GRANT, REVOKE e DENY ENDPOINT usa um ID de ponto de extremidade que o administrador deve obter da exibição de catálogo do ponto de extremidade.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria pontos de extremidade [!INCLUDE[tsql](../../includes/tsql-md.md)] para todos os protocolos de rede com suporte, bem como para a conexão de administrador dedicada.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] criados pela Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são os seguintes:  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] computador local  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] pipes nomeados  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] TCP padrão  
  
 Para obter mais informações sobre pontos de extremidade, veja [Configurar o Mecanismo de Banco de Dados para escutar em várias portas TCP](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md) e [Exibições de catálogo de pontos de extremidade &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql).  
  
 Para obter mais informações sobre configurações de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte o seguinte tópico nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [Configuração de rede do servidor](../../database-engine/configure-windows/server-network-configuration.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Configuração da Área de Superfície](../../relational-databases/security/surface-area-configuration.md)   
 [Considerações sobre segurança para uma instalação do SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [Planejando uma instalação do SQL Server](../../../2014/sql-server/install/planning-a-sql-server-installation.md)  
  
  
