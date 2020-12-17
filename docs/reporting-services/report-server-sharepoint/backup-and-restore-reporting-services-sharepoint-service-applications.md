---
title: Fazer backup e restaurar aplicativos de serviço SharePoint do Reporting Services | Microsoft Docs
description: Saiba como fazer backup e restaurar aplicativos de serviço do SQL Server Reporting Services usando a Administração Central do SharePoint ou o PowerShell.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: 559b88b776c92abfd98929f5b73cabb04a7f6d80
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474517"
---
# <a name="back-up-and-restore-reporting-services-sharepoint-service-applications"></a>Fazer backup e restaurar aplicativos de serviço SharePoint do Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Este tópico descreve como fazer backup de um aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e restaurá-lo usando a Administração Central do SharePoint ou o PowerShell.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

## <a name="before-you-begin"></a>Antes de começar

### <a name="limitations-and-restrictions"></a>Limitações e restrições

> [!NOTE]
>  Os aplicativos de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] podem ser parcialmente copiados em backup e restaurados usando a funcionalidade de backup e restauração do SharePoint. **São necessárias etapas adicionais** e as etapas são documentadas neste tópico. No momento, o processo de backup **não** faz backup das chaves de criptografia e credenciais para UEAs (contas de execução autônomas) ou a autenticação do Windows no banco de dados do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].

### <a name="recommendations"></a>Recomendações
  
-   Faça backup das chaves de criptografia antes de iniciar o backup do SharePoint. Se você não fizer backup das chaves de criptografia, não poderá acessar os dados criptografados, após a restauração do aplicativo de serviço. Você precisará excluir seus dados criptografados.  
  
-   Verifique se o aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] está usando a UEA ou a autenticação do Windows para acesso ao banco de dados. Se ele estiver usando uma delas, verifique quais são as credenciais apropriadas para que você possa configurar o aplicativo de serviço após o processo de restauração.  
  
-   Verifique se o log de backup do SharePoint foi criado na mesma pasta do arquivo de backup. O arquivo é geralmente nomeado **spbackup.log**  
  
## <a name="back-up-the-service-application"></a>Fazer backup do aplicativo de serviço

 Conclua as seguintes etapas nesta ordem:  
  
1.  Fazer backup das chaves de criptografia  
  
2.  Fazer backup do aplicativo de serviço  
  
3.  Verifique se o aplicativo de serviço usa uma UEA ou uma autenticação do Windows para acesso ao banco de dados. Em caso afirmativo, anote as credenciais a fim de que você possa usá-las para configurar o aplicativo de serviço depois que ele for restaurado.  

### <a name="back-up-the-encryption-keys-using-sharepoint-central-administration"></a>Fazer backup das chaves de criptografia usando a Administração Central do SharePoint

Para obter informações sobre como fazer backup de chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], confira a seção "Chaves de criptografia" de [Gerenciar um aplicativo do serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="back-up-the-service-application-using-sharepoint-central-administration"></a>Fazer backup do aplicativo de serviço usando a Administração Central do SharePoint

Para fazer backup do aplicativo de serviço, conclua as seguintes etapas:  
  
1.  Na Administração Central do SharePoint, selecione **Executar um backup** no grupo **Backup e Restauração**.  
  
2.  No nó **Serviços Compartilhados** , expanda **Aplicativos de Serviços Compartilhados** e selecione seu aplicativo de serviço. Seu tipo será **Aplicativo de Serviço SQL Server Reporting Services**.  
  
3.  Selecione **Avançar**.  
  
4.  Digite o caminho do **Local do backup:** e selecione **Iniciar Backup**  
  
5.  Repita o processo acima, mas em vez de selecionar o aplicativo de serviço, expanda o nó **Proxies de Serviços Compartilhados** e selecione o proxy do aplicativo de serviço. Seu tipo será **Proxy do Aplicativo de Serviço SQL Server Reporting Services**.  
  
 Para obter mais informações, consulte os seguintes tópicos na documentação do SharePoint:  
  
 [Backup de um aplicativo de serviço (SharePoint Foundation 2010) na documentação do SharePoint](/previous-versions/office/sharepoint-foundation-2010/ee748601(v=office.14)).  
  
 [Backup de um aplicativo de serviço (SharePoint Server 2010)](/SharePoint/administration/back-up-a-service-application)  
  
### <a name="verify-execution-account-and-database-authentication"></a>Verificar conta de execução e autenticação do banco de dados

 **Conta de execução:** para verificar se o aplicativo de serviço está usando uma conta de execução:  
  
1.  Na Administração Central do SharePoint, selecione **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo**.  
  
2.  Selecione o nome do aplicativo de serviço e, em seguida, **Gerenciar** na Faixa de Opções do SharePoint.  
  
3.  Selecione **Conta de Execução**.  
  
4.  Se uma conta de execução for configurada, você precisará saber as credenciais quando chegar a hora de restaurar o backup do aplicativo de serviço. Não continue com o procedimento de backup e restauração até que saiba as credenciais corretas.  
  
 **Autenticação de banco de dados:** para verificar se o aplicativo de serviço está usando a Autenticação do Windows para a autenticação do banco de dados:  
  
1.  Na Administração Central do SharePoint, selecione **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo**.  
  
2.  Selecione o nome do aplicativo de serviço e, em seguida, **Propriedades** na Faixa de Opções do SharePoint.  
  
3.  Leia a seção **Banco de Dados do Serviço SQL Server Reporting Services** .  
  
4.  Se a Autenticação do Windows estiver configurada, você precisará saber as credenciais para que possa configurar o aplicativo de serviço após sua restauração. Não continue com o procedimento de backup e restauração até que saiba as credenciais corretas.  
  
## <a name="restore-the-service-application"></a>Restaurar o aplicativo de serviço

 Conclua as seguintes etapas nesta ordem:  
  
1.  Restaurar o aplicativo de serviço [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
2.  Restaurar as chaves de criptografia  
  
3.  Se seu aplicativo de serviço estava usando uma conta de execução ou uma autenticação do Windows para acesso ao banco de dados, configure as credenciais.  
  
### <a name="restore-the-service-application-using-sharepoint-central-administration"></a>Restaurar o aplicativo de serviço usando a Administração Central do SharePoint
  
1.  Na Administração Central do SharePoint, selecione **Restaurar de um backup** no grupo **Backup e Restauração**.  
  
2.  Digite o caminho para o arquivo de backup na caixa **Local do Diretório de Backup** e selecione **Atualizar**.  
  
3.  Selecione o backup do aplicativo de serviço na lista **Componente Superior** e, em seguida, selecione **Avançar**.  
  
4.  Selecione o aplicativo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e, em seguida, **Avançar**.  
  
5.  Na seção **Nomes e Senhas de Logon** , digite a senha para o nome de logon. A caixa de nome de logon deve ser populada com o logon que o aplicativo de serviço estava usando antes do backup.  
  
6.  Selecione **Iniciar Restauração**.  
  
7.  Repita o processo acima, mas em vez de restaurar o aplicativo de serviço, expanda o nó **Serviços Compartilhados** e selecione o nó **Aplicativos de Serviços Compartilhados** .  
  
 Para obter mais informações, consulte os seguintes tópicos na documentação do SharePoint:  
  
 [Restauração de um aplicativo de serviço (SharePoint Foundation 2010)](/previous-versions/office/sharepoint-foundation-2010/ee748615(v=office.14)).  
  
 [Restauração de um aplicativo de serviço (SharePoint Server 2010)](/SharePoint/administration/restore-a-service-application).  

### <a name="restore-the-encryption-keys-using-sharepoint-central-administration"></a>Restaurar as chaves de criptografia usando a Administração Central do SharePoint

 Para obter informações sobre como restaurar chaves de criptografia do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], confira a seção "Chaves de criptografia" de [Gerenciar um aplicativo do serviço SharePoint do Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  

### <a name="configure-the-execution-account-and-database-authentication"></a>Configurar a conta de execução e a autenticação do banco de dados

 **Conta de execução:** se o aplicativo de serviço estava usando uma conta de execução, execute as seguintes etapas para configurá-lo:  
  
1.  Na Administração Central do SharePoint, selecione **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo**.  
  
2.  Selecione o nome do aplicativo de serviço e, em seguida, **Gerenciar** na Faixa de Opções do SharePoint.  
  
3.  Selecione **Conta de Execução**.  
  
4.  Digite a conta e a senha, e selecione a caixa **Especificar uma Conta de Execução** .  
  
5.  Selecione **OK**.  
  
 **Autenticação de banco de dados:** se o aplicativo de serviço estava usando a Autenticação do Windows para autenticação do banco de dados, execute as seguintes etapas:  
  
1.  Na Administração Central do SharePoint, selecione **Gerenciar Aplicativos de Serviço** no grupo **Gerenciamento de Aplicativo**.  
  
2.  Selecione o nome do aplicativo de serviço e, em seguida, **Propriedades** na Faixa de Opções do SharePoint.  
  
3.  Leia a seção **Banco de Dados do Serviço SQL Server Reporting Services** .  
  
4.  Selecione **Autenticação do Windows**.  
  
5.  Digite a conta e senha. Selecione **Uso como Credenciais do Windows** , se apropriado.  
  
6.  Selecione **Ok**

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)