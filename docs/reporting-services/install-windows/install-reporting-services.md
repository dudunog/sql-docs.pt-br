---
description: Instale o SQL Server Reporting Services
title: Instalar o SQL Server Reporting Services | Microsoft Docs
ms.date: 05/01/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 74713128e0a7e1c749bcde676d02c63ec05e3632
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891926"
---
# <a name="install-sql-server-reporting-services"></a>Instale o SQL Server Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2017-and-later](../../includes/ssrs-appliesto-2017-and-later.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

A instalação do SQL Server Reporting Services envolve componentes do servidor para armazenar itens de relatório, renderizar relatórios, processar assinaturas e outros serviços de relatório. 

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
Baixe o [SQL Server 2019 Reporting Services](https://www.microsoft.com/download/details.aspx?id=100122) do Centro de Download da Microsoft.

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Baixe o [SQL Server 2017 Reporting Services](https://www.microsoft.com/download/details.aspx?id=55252) do Centro de Download da Microsoft.

::: moniker-end

> [!NOTE]
> Procurando o Servidor de Relatórios do Power BI? Consulte [Instalar o Servidor de Relatórios do Power BI](https://powerbi.microsoft.com/documentation/reportserver-install-report-server/).
> 
> Atualizando ou migrando de um SQL Server 2016 ou de uma versão anterior do Reporting Services? Confira [Atualizar e migrar o Reporting Services](upgrade-and-migrate-reporting-services.md).

## <a name="before-you-begin"></a>Antes de começar

Antes de instalar o Reporting Services, examine os [Requisitos de hardware e software para instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).

## <a name="install-your-report-server"></a>Instalar o servidor de relatório

A instalação de um servidor de relatório é simples. Há apenas algumas etapas para instalar os arquivos.

> [!NOTE]
> Não é necessário ter um servidor do Mecanismo de Banco de Dados do SQL Server disponível no momento da instalação. Você precisará de um para configurar o Reporting Services após a instalação.

1. Encontre o local do SQLServerReportingServices.exe e inicie o instalador.

2. Selecione **Instalar o Reporting Services**.

3. Escolha uma edição a ser instalada e, em seguida, selecione **Avançar**.

    Para obter uma edição gratuita, escolha Evaluation ou Developer na lista suspensa.

    ![Evaluation ou Developer Editions](media/install-reporting-services/report-server-install-edition-select.png)

    Caso contrário, insira uma chave do produto (Product Key). [Localize a chave do produto (Product Key) para o SQL Server Reporting Services](find-reporting-services-product-key-ssrs.md).

4. Leia e concorde com os termos e condições de licença e, em seguida, selecione **Avançar**.

5. É necessário ter um Mecanismo de Banco de Dados disponível para armazenar o banco de dados do servidor de relatório. Selecione **Avançar** para instalar somente o servidor de relatório.

6. Especifique o local de instalação do servidor de relatório. Selecione **Instalar** para continuar.

    > [!NOTE]
    > O caminho padrão é C:\Program Files\Microsoft SQL Server Reporting Services.

7. Após uma instalação bem-sucedida, selecione **Configurar Servidor de Relatório** para iniciar o Gerenciador de Configurações do Servidor de Relatório.

## <a name="configure-your-report-server"></a>Configurar o servidor de relatório

Depois de selecionar **Configurar Servidor de Relatório** na instalação, você verá o **Gerenciador de Configurações do Servidor de Relatório**. Para obter mais informações, consulte [Gerenciador de Configurações do Servidor de Relatório](reporting-services-configuration-manager-native-mode.md).

É necessário [criar um banco de dados do servidor de relatório](ssrs-report-server-create-a-report-server-database.md) para concluir a configuração inicial do Reporting Services. Um servidor de Banco de Dados do SQL Server é necessário para concluir esta etapa.

### <a name="creating-a-database-on-a-different-server"></a>Criando um banco de dados em outro servidor

Caso você esteja criando o banco de dados do servidor de relatório em um servidor de banco de dados em outro computador, precisará alterar a conta de serviço do servidor de relatório para uma credencial que é reconhecida no servidor de banco de dados.

Por padrão, o servidor de relatório usa a conta de serviço virtual. Se você tentar criar um banco de dados em outro servidor, poderá receber o erro a seguir durante a etapa Aplicando direitos de conexão.

`System.Data.SqlClient.SqlException (0x80131904): Windows NT user or group '(null)' not found. Check the name again.`

Para solucionar o erro, altere a conta de serviço para Serviço de Rede ou uma conta de domínio. A alteração da conta de serviço para Serviço de Rede aplica os direitos no contexto da conta do computador do servidor de relatório.

Para obter mais informações, consulte [Configurar a conta de serviço do servidor de relatório](configure-the-report-server-service-account-ssrs-configuration-manager.md).

## <a name="windows-service"></a>Windows Service

Um serviço Windows é criado como parte da instalação. Ele é exibido como **SQL Server Reporting Services**. O nome do serviço é **SQLServerReportingServices**.

## <a name="default-url-reservations"></a>Reservas de URL padrão

As reservas de URL são compostas de um prefixo, nome de host, porta e diretório virtual:

|Parte|Descrição|
|----------|-----------------|
|Prefixo|O prefixo padrão é HTTP. Se você instalou anteriormente um certificado de protocolo TLS (Transport Layer Security), antes conhecido como SSL (Secure Sockets Layer), a Instalação tentará criar reservas de URL que usam o prefixo HTTPS.|
|Nome do host|O nome de host padrão é um curinga forte (+). Ele especifica que o servidor de relatório aceita qualquer solicitação HTTP na porta designada para qualquer nome do host resolvido para o computador, incluindo `https://<computername>/reportserver`, `https://localhost/reportserver` ou `https://<IPAddress>/reportserver.`|
|Porta|A porta padrão é 80. Se você usar qualquer porta que não seja a 80, precisará adicioná-la explicitamente à URL quando abrir o portal da Web em uma janela do navegador.|
|Diretório virtual|Por padrão, os diretórios virtuais são criados no formato de ReportServer para o serviço Web Servidor de Relatórios e Reports para o portal da Web. Para o serviço Web Servidor de Relatórios, o diretório virtual padrão é **reportserver**. Para o portal da Web, o diretório virtual padrão é **reports**.|

Um exemplo de cadeia de caracteres de URL completa poderia ser como segue:

- `https://+:80/reportserver`, fornece acesso ao servidor de relatório.

- `https://+:80/reports`, fornece acesso ao portal da Web.

## <a name="firewall"></a>Firewall

Se estiver acessando o servidor de relatório em um computador remoto, é recomendável verificar se você configurou regras de firewall caso haja um firewall presente.

Você precisa abrir a porta TCP configurada para a URL do Serviço Web e a URL do Portal da Web. Por padrão, elas são configuradas na porta TCP 80.

## <a name="additional-configuration"></a>Configuração adicional

- Para configurar a integração com o serviço do Power BI, de modo que você possa fixar itens de relatório em um painel do Power BI, consulte [Integrar com o serviço do Power BI](power-bi-report-server-integration-configuration-manager.md).

- Para configurar o email para o processamento de assinaturas, consulte [Configurações de email](e-mail-settings-reporting-services-native-mode-configuration-manager.md) e [Entrega de email em um servidor de relatório](../subscriptions/e-mail-delivery-in-reporting-services.md).

- Para configurar o portal da Web para que você possa acessá-lo em um computador remoto a fim de exibir e gerenciar relatórios, consulte [Configurar um firewall para acesso ao servidor de relatório](../report-server/configure-a-firewall-for-report-server-access.md) e [Configurar um servidor de relatório para administração remota](../report-server/configure-a-report-server-for-remote-administration.md).

## <a name="related-information"></a>Informações relacionadas

Para obter informações sobre como instalar o SQL Server Reporting Services no modo nativo, confira [Instalar o servidor de relatório no modo nativo do Reporting Services](install-reporting-services-native-mode-report-server.md). 

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

Para obter informações sobre como instalar o SQL Server 2016 Reporting Services (e versões anteriores) no modo de integração do SharePoint, confira [Instalar o primeiro Servidor de Relatório no modo do SharePoint](install-the-first-report-server-in-sharepoint-mode.md).

::: moniker-end

## <a name="next-steps"></a>Próximas etapas

Com o servidor de relatório instalado, comece a criar relatórios e implante-os no servidor de relatório. Para obter informações sobre como começar a usar o Construtor de Relatórios, consulte [Instalar o Construtor de Relatórios](../../reporting-services/install-windows/install-report-builder.md).

Para criar relatórios usando o SQL Server Data Tools, [baixe o SQL Server Data Tools](https://go.microsoft.com/fwlink/?LinkID=616714).

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
