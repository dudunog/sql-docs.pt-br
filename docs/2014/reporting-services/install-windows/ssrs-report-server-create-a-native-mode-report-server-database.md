---
title: Criar um banco de dados do servidor de relatório no modo nativo (Gerenciador de Configurações do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- report servers [Reporting Services], databases
- databases [Reporting Services], creating
ms.assetid: 81b9f4ad-800b-4688-8b47-a5a83dc8ff10
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ae243786119823a7be4a093fcfef232f58d8492
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108682"
---
# <a name="create-a-native-mode-report-server-database--ssrs-configuration-manager"></a>Criar um banco de dados de servidor de relatório no modo nativo (Gerenciador de configurações do SSRS)
  O Modo Nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para armazenamento interno. O banco de dados é necessário e é usado para armazenar relatórios publicados, modelos, fontes de dados compartilhadas, dados de sessão, recursos e metadados do servidor.  
  
 Para criar um banco de dados de servidor de relatório ou alterar as credenciais ou a cadeia de caracteres de conexão, use as opções na página Banco de Dados do Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo|  
  
## <a name="when-to-create-or-configure-the-report-server-databases"></a>Quando criar ou configurar os bancos de dados do servidor de relatório  
 Você deve criar e configurar o banco de dados do servidor de relatório se instalou o servidor de relatório no modo somente arquivos.  
  
 Se você instalou o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na configuração padrão para o modo nativo, o banco de dados do servidor de relatório foi criado e configurado automaticamente quando a instância do servidor de relatório foi instalada. É possível usar o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para exibir ou modificar as configurações que a Instalação configurou para você.  
  
##  <a name="before-you-start"></a><a name="rsdbrequirements"></a> Antes de iniciar  
 Criar ou configurar um banco de dados de servidor de relatório é um processo de várias etapas. Antes de criar o banco de dados do servidor de relatório, considere como você deseja especificar os seguintes itens:  
  
 Selecionar um servidor de banco de dados  
 Examine as versões com suporte do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e as edições com suporte no tópico [Criar um banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md).  
  
 Habilitar conexões TCP/IP  
 Habilite conexões TCP/IP para o [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Algumas edições do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não habilitam TCP/IP por padrão. As instruções são fornecidas neste tópico.  
  
 Abrir porta para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Para um servidor remoto, se você estiver usando software de firewall, deverá abrir a porta na qual o [!INCLUDE[ssDE](../../includes/ssde-md.md)] escuta.  
  
 Decidir sobre credenciais do servidor de relatório  
 Decida como o servidor de relatório irá se conectar aos bancos de dados do servidor de relatório. Os tipos de credencial incluem conta de usuário do domínio, conta de usuário do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou a conta de serviço do Servidor de Relatório.  
  
 Essas credenciais são criptografadas e armazenadas no arquivo RSReportServer.config. O servidor de relatório usa essas credenciais para conexões contínuas com o banco de dados do servidor de relatório. Para usar uma conta de usuário do Windows ou uma conta de usuário do banco de dados, especifique uma já existente. Embora o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] crie um logon e defina as permissões necessárias, ele não criará uma conta para você. Para obter mais informações, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
 Escolher um idioma do servidor de relatório  
 Escolha um idioma a ser especificado para o servidor de relatório. Os nomes de função predefinidos, as descrições e as pastas Meus Relatórios não aparecem em idiomas diferentes quando usuários se conectam ao servidor usando versões de idiomas diferentes de um navegador.  
  
 Verificar credenciais para criar e provisionar o banco de dados  
 Verifique se você tem credenciais de conta com permissão para criar bancos de dados na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Essas credenciais são usadas para uma conexão única a fim de criar o banco de dados do servidor de relatório e **RSExecRole**. Se um logon ainda não existir, um logon de usuário do banco de dados será criado para a conta usada pelo servidor de relatório para conectar-se ao banco de dados. Você pode conectar-se sob a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows com a qual efetuou logon ou pode inserir um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-enable-access-to-a-remote-report-server-database"></a>Para habilitar o acesso a um banco de dados do servidor de relatório remoto  
  
1.  Se você estiver usando uma instância remota do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , efetue logon no servidor de banco de dados para verificar ou habilitar conexões TCP/IP.  
  
2.  Aponte para **Iniciar**, aponte para **Todos os Programas**, aponte para **Microsoft SQL Server**aponte para **Ferramentas de Configuração**e clique em **SQL Server Configuration Manager**.  
  
3.  Abra **SQL Server configuração de rede**.  
  
4.  Selecione a instância.  
  
5.  Clique com o botão direito do mouse em **TCP/IP** e clique em **habilitado**.  
  
6.  Reinicie o serviço.  
  
7.  Abra seu software de firewall e abra a porta na qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta. Para a instância padrão, usa-se geralmente a porta 1433 para conexões TCP/IP. Para obter mais informações, veja [Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="to-create-a-local-report-server-database"></a>Para criar um banco de dados de servidor de relatório local  
  
1.  Inicie o Gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se à instância do servidor de relatório para a qual você está criando o banco de dados. Para obter mais informações, consulte [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
2.  Na página Banco de Dados, clique em **Alterar Banco de Dados**.  
  
3.  Clique em **criar um novo banco de dados do servidor de relatório**e clique em **Avançar**.  
  
4.  Conecte-se à instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que você usará para criar e hospedar o banco de dados do servidor de relatório:  
  
    1.  Digite a instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] que deseja usar. O assistente exibirá um [!INCLUDE[ssDE](../../includes/ssde-md.md)] local que é executado como a instância padrão, se estiver disponível. Caso contrário, você deverá digitar o servidor e a instância a serem usados. As instâncias nomeadas são especificadas neste formato: \<servername>\\<instancename\>.  
  
    2.  Insira as credenciais usadas para uma conexão única com o [!INCLUDE[ssDE](../../includes/ssde-md.md)] com a finalidade de criar os bancos de dados do servidor de relatório. Para obter mais informações sobre como essas credenciais são usadas, consulte [Antes de iniciar](#rsdbrequirements) neste tópico.  
  
    3.  Clique em **Testar Conexão** para validar a conexão com o servidor.  
  
    4.  Clique em **Avançar**.  
  
5.  Especifique as propriedades usadas para criar o banco de dados. Para obter mais informações sobre como essas propriedades são usadas, consulte [Antes de iniciar](#rsdbrequirements) neste tópico:  
  
    1.  Digite o nome do banco de dados do servidor de relatório. Um banco de dados temporário será criado juntamente com o banco de dados primário. Considere a possibilidade de usar um nome descritivo que o ajude a se lembrar de como o banco de dados é usado. O nome especificado será usado durante todo o tempo de vida do banco de dados. Não é possível renomear um banco de dados de servidor de relatório depois que ele for criado.  
  
    2.  Selecione o idioma no qual deseja que as definições de função e Meus Relatórios sejam exibidas.  
  
    3.  O Modo de Servidor de Relatório sempre é definido como **Nativo**.  
  
    4.  Clique em **Avançar**.  
  
6.  Especifique as credenciais usadas pelo servidor de relatório para conectar-se ao banco de dados do servidor de relatório.  
  
    1.  Especifique o tipo de autenticação:  
  
         Selecione **Credenciais do Banco de Dados** para conectar-se usando um logon de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que já esteja definido. O uso de credenciais do banco de dados é recomendado se o servidor de relatório estiver em um computador que esteja em um domínio diferente, em um domínio não confiável ou atrás de um firewall.  
  
         Selecione **Credenciais do Windows** se tiver uma conta de usuário de domínio com menor privilégio que tenha permissão para efetuar logon no computador e no servidor de banco de dados.  
  
         Selecione **Credenciais de Serviço** para que o servidor de relatório se conecte usando sua conta de serviço. Com essa opção, o servidor se conecta usando segurança integrada; as credenciais não são criptografadas ou armazenadas.  
  
    2.  Clique em **Avançar**.  
  
7.  Revise as informações na página Resumo para verificar se as configurações estão corretas e clique em **Avançar**.  
  
8.  Verifique a conexão clicando em uma URL na página URL do Servidor de Relatório ou na página URL do Gerenciador de Relatórios. As URLs devem estar definidas para que esse teste funcione. Se a conexão do banco de dados do servidor de relatório for válida, você verá a hierarquia de pastas do servidor de relatório ou o Gerenciador de Relatórios em uma janela do navegador. Para obter mais informações, veja [Verificar uma instalação do Reporting Services](verify-a-reporting-services-installation.md) nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;Configuration Manager SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Banco de dados &#40;modo nativo do SSRS&#41;](../../sql-server/install/database-ssrs-native-mode.md)   
 [Gerenciar um Reporting Services servidor de relatório no modo nativo](../report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)  
  
  
