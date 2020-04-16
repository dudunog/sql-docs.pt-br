---
title: Configure uma conta de serviço (SSRS Configuration Manager) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Server Web service, accounts
- service accounts [Reporting Services]
- Report Server Windows service, accounts
- Web service [Reporting Services], report server
ms.assetid: 25000ad5-3f80-4210-8331-d4754dc217e0
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 04dff943d1227f84ff514e593f65c2ce4d7a918f
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/15/2020
ms.locfileid: "71952579"
---
# <a name="configure-a-service-account-ssrs-configuration-manager"></a>Configurar uma conta de serviço (Gerenciador de configurações do SSRS)
  Em uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o serviço Web Servidor de Relatório, o Gerenciador de Relatórios e o aplicativo de processamento em segundo plano são executados em um único serviço. A conta em que o serviço é executado é definida durante a Instalação quando você especifica a conta na página Identidade do Serviço, mas é possível usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se desejar usar uma conta diferente ou atualizar a senha.  
  
 Se você tiver um servidor de relatório saqueado para usar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo SharePoint Integrated e alterar a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] conta de serviço usando a ferramenta Configuração, você também deve abrir a Administração Central do SharePoint e usar a página De acesso ao banco de **dados de concessão** para reaplicar as configurações do servidor de relatório e da instância. Esta etapa concederá à nova conta de serviço acesso aos bancos [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]de dados SharePoint, que é necessário para se integrar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] com ou .  
  
 Sempre use a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para atualizar a conta de serviço, de forma que outras configurações que dependam da identidade de serviço possam ser atualizadas simultaneamente.  
  
> [!NOTE]  
>  Não há suporte para contas de serviço internas do Windows (Serviço Local ou Serviço de Rede) como contas de serviço do servidor de relatório em um computador que seja controlador de domínio.  
  
 Procedimentos  
  
### <a name="to-configure-the-report-server-service-account"></a>Para configurar a conta de serviço do Servidor de Relatório  
  
1.  Inicie o gerenciador de Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e conecte-se ao servidor de relatório.  
  
2.  Na página Conta de Serviço, selecione a opção que descreve o tipo de conta que você deseja usar. Para obter recomendações sobre qual tipo de conta especificar, consulte [Configurar a conta de serviço do servidor de relatório &#40;o SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
3.  Se você tiver selecionado uma conta de usuário do Windows, especifique a nova conta e a senha. A conta não pode ter mais do que 20 caracteres.  
  
     Se o servidor de relatório for implantado em uma rede que ofereça suporte à autenticação Kerberos, você deverá registrar o SPN (Nome da Entidade de Serviço) do servidor de relatório com a conta de usuário do domínio recém-especificada. Para obter mais informações, consulte [Registrar um SPN &#40;Nome da Entidade de Serviço&#41; para um servidor de relatório](../../reporting-services/report-server/register-a-service-principal-name-spn-for-a-report-server.md).  
  
4.  Clique em **Aplicar**.  
  
5.  Quando for solicitado que você faça backup da chave simétrica, digite um nome e um local de arquivo para o backup da chave simétrica, digite uma senha para bloquear e desbloquear o arquivo e clique em **OK**.  
  
6.  Se o servidor de relatório usar a conta de serviço para se conectar ao banco de dados do servidor de relatório, as informações de conexão serão atualizadas para usar a nova conta ou senha. A atualização das informações da conexão exige que você se conecte ao banco de dados. Se a caixa de diálogo  **Conexão de Banco de Dados** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for exibida, insira as credenciais que têm permissão para se conectar ao banco de dados e, em seguida, clique em **OK**.  
  
7.  Quando for avisado para restaurar a chave simétrica, digite a senha que você especificou na etapa 5 e clique em **OK**.  
  
8.  Revise as mensagens de status no painel Resultados para verificar se todas as tarefas foram concluídas com êxito.  
  
## <a name="troubleshooting-service-identity-update-errors"></a>Solucionando problemas de erros de atualização de identidade do serviço  
 A alteração da identidade do serviço inicia uma série de eventos que incluem o reinício do serviço, a atualização da chave de criptografia protegida por senha, a atualização das reservas de URL e a atualização das informações de conexão do banco de dados do servidor de relatório, caso você esteja usando a conta de serviço para se conectar ao banco de dados do servidor de relatório. Você pode monitorar o status desses eventos pela exibição das notificações no painel Resultados, na parte inferior da página. Se ocorrerem erros durante esse processo, você poderá tentar resolvê-los usando as seguintes técnicas:  
  
-   Se a chave simétrica não puder ser restaurada, você poderá tentar restaurá-la manualmente usando a opção **Restaurar** na página Chaves de criptografia. Se isso não funcionar, considere a exclusão do conteúdo criptografado. Você precisará recriar as informações de conexão da fonte de dados e as assinaturas, mas o restante do seu conteúdo ainda estará disponível. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
-   Se o serviço não for iniciado, reinicie-o manualmente usando o aplicativo de console Serviços em Ferramentas do Administrador.  
  
-   Podem ocorrer erros de reserva de URL ao atualizar a conta de serviço. Cada reserva de URL inclui um descritor de segurança que inclui uma DACL (Lista de Controle de Acesso Discricionário) que concede permissão à conta de serviço para aceitar solicitações na URL. Quando você atualizar a conta, a URL deverá ser recriada a fim de atualizar a DACL com as novas informações de conta. Se a reserva de URL não puder ser recriada e você souber que a conta é válida, tente reiniciar o computador. Se o erro persistir, tente usar uma conta diferente.  
  
## <a name="see-also"></a>Consulte Também  
 [O gerenciador de configuração de serviços de relatórios &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configure a conta de serviço do servidor de relatório &#40;o gerenciador de configuração SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configure uma conexão de banco de dados do servidor de relatórios &#40;o gerenciador de configuração SSRS&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Conta de serviço &#40;modo nativo SSRS&#41;](../../../2014/sql-server/install/service-account-ssrs-native-mode.md)   
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
