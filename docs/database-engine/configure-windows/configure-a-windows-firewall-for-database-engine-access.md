---
title: Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados | Microsoft Docs
description: Saiba como configurar um Firewall do Windows para que os computadores cliente possam acessar uma instância do Mecanismo de Banco de Dados do SQL Server por meio do firewall.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], firewall systems
- firewall systems, [Database Engine]
- security [SQL Server], firewalls
ms.assetid: 0093b43c-c6b5-4574-9b30-3a0e91e1a1f9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c1d9b69cc55ab617eb3a4c5b4ed2ebb27726f35b
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91669726"
---
# <a name="configure-a-windows-firewall-for-database-engine-access"></a>Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]


  Este tópico descreve como configurar um firewall de Windows para acesso ao Mecanismo de Banco de Dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Os sistemas de Firewall ajudam a impedir o acesso não autorizado aos recursos do computador. Para acessar uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] através de um firewall, é necessário configurar o firewall no computador que estiver executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações sobre as configurações padrão do Firewall do Windows e uma descrição das portas TCP que afetam o [!INCLUDE[ssDE](../../includes/ssde-md.md)], Analysis Services, o Reporting Services e o Integration Services, veja [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md). Há muitos sistemas de firewall disponíveis. Para obter informações específicas para o seu sistema, consulte a documentação do firewall.  
  
 As etapas principais para permitir acesso são:  
  
1.  Configurar o [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar uma porta TCP/IP específica. A instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa a porta 1433, mas isso pode ser alterado. A porta usada pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] é listada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], do [!INCLUDE[ssEW](../../includes/ssew-md.md)] e instâncias nomeadas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] usam portas dinâmicas. Para configurar essas instâncias para usar uma porta específica, consulte [Configurar um servidor para escuta em uma porta TCP específica &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
2.  Configurar o firewall para permitir que usuários ou computadores autorizados tenham acesso a essa porta.  
  
> [!NOTE]  
>  O serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite que os usuários se conectem a instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que não estejam escutando na porta 1433, sem conhecer o número da porta. Para usar o Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , abra a porta UDP 1434. Para promover um ambiente mais seguro, deixe o serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] parado e configure clientes para que se conectem por meio do número da porta.  
  
> [!NOTE]  
>  Por padrão, o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows habilita o Firewall do Windows, que fecha a porta 1433 para impedir que computadores da Internet se conectem a uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no seu computador. As conexões com a instância padrão por meio de TCP/IP não são possíveis, a menos que você reabra a porta 1433. As etapas básicas para configurar o firewall do Windows XP são fornecidas nos procedimentos a seguir. Para obter mais informações, consulte a documentação do Windows.  
  
 Como alternativa para configurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para escutar em uma porta fixa e abrir a porta, você pode listar o executável do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Sqlservr.exe) como uma exceção aos programas bloqueados. Use este método quando quiser continuar usando portas dinâmicas. Apenas uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser acessada dessa maneira.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados usando:**  
  
     [SQL Server Configuration Manager](#SSMSProcedure)  
  
## <a name="before-you-begin"></a>Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 A abertura de portas no firewall pode deixar o servidor exposto a ataques mal-intencionados. Certifique-se de conhecer os sistemas de firewall antes de abrir portas. Para obter mais informações, consulte [Security Considerations for a SQL Server Installation](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
 Aplica-se ao Windows Vista, Windows 7 e Windows Server 2008  
  
 Os procedimentos a seguir configuram o Firewall do Windows com o uso do Firewall do Windows com o snap-in MMC (Console de Gerenciamento Microsoft) de Segurança Avançada. O Firewall do Windows com Segurança Avançada configura apenas o perfil atual. Para obter mais informações sobre o Firewall do Windows com Segurança Avançada, consulte [Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access"></a>Para abrir uma porta no firewall do Windows para acesso TCP  
  
1.  No menu **Iniciar** , clique em **Executar**, digite **WF.msc**e clique em **OK**.  
  
2.  No **Firewall do Windows com Segurança Avançada**, no painel esquerdo, clique com o botão direito do mouse em **Regras de Entrada** e, em seguida, clique em **Nova Regra** no painel de ações.  
  
3.  Na caixa de diálogo **Tipo de Regra** , selecione **Porta**e clique em **Avançar**.  
  
4.  Na caixa de diálogo **Protocolo e Portas** , selecione **TCP**. Selecione **Portas locais específicas**e digite o número da porta da instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], por exemplo, **1433** para a instância padrão. Clique em **Próximo**.  
  
5.  Na caixa de diálogo **Ação**, selecione **Permitir a conexão** e clique em **Avançar**.  
  
6.  Na caixa de diálogo **Perfil** , selecione quaisquer perfis que descrevam o ambiente de conexão do computador quando você deseja se conectar ao [!INCLUDE[ssDE](../../includes/ssde-md.md)]e clique em **Avançar**.  
  
7.  Na caixa de diálogo **Nome**, digite um nome e uma descrição para essa regra, e clique em **Concluir**.  
  
#### <a name="to-open-access-to-sql-server-when-using-dynamic-ports"></a>Para abrir o acesso ao SQL Server durante o uso de portas dinâmicas  
  
1.  No menu **Iniciar** , clique em **Executar**, digite **WF.msc**e clique em **OK**.  
  
2.  No **Firewall do Windows com Segurança Avançada**, no painel esquerdo, clique com o botão direito do mouse em **Regras de Entrada** e, em seguida, clique em **Nova Regra** no painel de ações.  
  
3.  Na caixa de diálogo **Tipo de Regra** , selecione **Programa**e clique em **Avançar**.  
  
4.  Na caixa de diálogo **Programa** , selecione **Este caminho de programa**. Clique em **Procurar**, navegue até a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você deseja acessar pelo firewall e clique em **Abrir**. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em **C:\Arquivos de Programas\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\Sqlservr.exe**. Clique em **Próximo**.  
  
5.  Na caixa de diálogo **Ação**, selecione **Permitir a conexão** e clique em **Avançar**.  
  
6.  Na caixa de diálogo **Perfil** , selecione quaisquer perfis que descrevam o ambiente de conexão do computador quando você deseja se conectar ao [!INCLUDE[ssDE](../../includes/ssde-md.md)]e clique em **Avançar**.  
  
7.  Na caixa de diálogo **Nome**, digite um nome e uma descrição para essa regra, e clique em **Concluir**.  
  
## <a name="see-also"></a>Consulte Também  
 [Como: definir as configurações do firewall (Banco de Dados SQL do Azure)](/azure/azure-sql/database/firewall-configure)  
  
