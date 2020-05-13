---
title: 'RHEL: Instalar o SQL Server em Linux'
titleSuffix: SQL Server
description: Este início rápido mostra como instalar o SQL Server 2017 ou o SQL Server 2019 no RHEL (Red Hat Enterprise Linux) e, em seguida, criar e consultar um banco de dados com sqlcmd.
author: VanMSFT
ms.custom: seo-lt-2019
ms.author: vanto
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 92503f59-96dc-4f6a-b1b0-d135c43e935e
ms.openlocfilehash: 55bdeab8f54b8aca9aea83cc0e4b1cb2c780da56
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760642"
---
# <a name="quickstart-install-sql-server-and-create-a-database-on-red-hat"></a>Início Rápido: Instalar o SQL Server e criar um banco de dados no Red Hat

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

Neste início rápido, você instalará o SQL Server 2017 ou o SQL Server 2019 no RHEL (Red Hat Enterprise Linux). Em seguida, você se conecta ao **sqlcmd** parar criar seu primeiro banco de dados e executar consultas.

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

Neste início rápido, você instala o SQL Server 2019 no Red Hat Enterprise Linux (RHEL) 8. Em seguida, você se conecta ao **sqlcmd** parar criar seu primeiro banco de dados e executar consultas.

::: moniker-end

> [!TIP]
> Este tutorial requer a entrada do usuário e uma conexão com a Internet. Se estiver interessado nos procedimentos de instalação [autônoma](sql-server-linux-setup.md#unattended) ou [offline](sql-server-linux-setup.md#offline), confira [Diretrizes de instalação para o SQL Server em Linux](sql-server-linux-setup.md).

## <a name="prerequisites"></a>Pré-requisitos

É necessário ter um computador RHEL 7.3, 7.4, 7.5, 7.6 ou 8 com **pelo menos 2 GB** de memória.

Para instalar o Red Hat Enterprise Linux em seu próprio computador, acesse [https://access.redhat.com/products/red-hat-enterprise-linux/evaluation](https://access.redhat.com/products/red-hat-enterprise-linux/evaluation). Também é possível criar máquinas virtuais RHEL no Azure. Confira [Criar e gerenciar VMs do Linux com a CLI do Azure](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-manage-vm) e use `--image RHEL` na chamada para `az vm create`.

Se você já tiver instalado uma versão CTP ou RC do SQL Server, será necessário remover primeiro o repositório antigo antes de seguir essas etapas. Para saber mais, confira [Configurar repositórios do Linux para o SQL Server 2017 e 2019](sql-server-linux-change-repo.md).

Para obter outros requisitos do sistema, confira [Requisitos do sistema do SQL Server em Linux](sql-server-linux-setup.md#system).

<!--SQL Server 2017 on Linux-->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

## <a name="install-sql-server"></a><a id="install"></a>Instalar o SQL Server

> [!NOTE]
> O RHEL 8 tem suporte no SQL Server 2017 a partir da CU20. Os comandos do SQL Server 2017 a seguir apontam para o repositório do RHEL 8. O RHEL 8 não vem pré-instalado com o Python 2, que é exigido pelo SQL Server. Antes de começar as etapas de instalação do SQL Server, execute o comando e verifique se python2 está selecionado como o interpretador:
>
> ```
> sudo alternatives --config python
> # If not configured, install python2 and openssl10 using the following commands: 
> sudo yum install python2
> sudo yum install compat-openssl10
> # Configure python2 as the default interpreter using this command: 
> sudo alternatives --config python
> ```
> Para obter mais informações, consulte blog a seguir sobre como instalar o Python 2 e configurá-lo como o interpretador padrão: https://www.redhat.com/en/blog/installing-microsoft-sql-server-red-hat-enterprise-linux-8-beta.
>
> Se você estiver usando o RHEL 7, altere o caminho abaixo para `/rhel/7` em vez de `/rhel/8`.

Para configurar o SQL Server no RHEL, execute os seguintes comandos em um terminal para instalar o pacote **mssql-server**:

1. Baixe o arquivo de configuração do repositório do Red Hat do Microsoft SQL Server 2017:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2017.repo
   ```

   > [!TIP]
   > Se quiser instalar o SQL Server 2019, você precisará registrar o repositório do SQL Server 2019. Use o seguinte comando para a instalações do SQL Server 2019:
   >
   > ```bash
   > sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo
   > ```

2. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Após a conclusão da instalação do pacote, execute a **instalação de mssql-conf** e siga os prompts para definir a senha SA e escolher sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!TIP]
   > As seguintes edições do SQL Server 2017 são licenciadas gratuitamente: Evaluation, Developer e Express.

   > [!NOTE]
   > Especifique uma senha forte para a conta SA (comprimento mínimo de 8 caracteres, incluindo letras maiúsculas e minúsculas, 10 dígitos básicos e/ou símbolos não alfanuméricos).

4. Após concluir a configuração, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

5. Para permitir conexões remotas, abra a porta do SQL Server no firewall no RHEL. A porta do SQL Server padrão é TCP 1433. Se você estiver usando **FirewallD** para o firewall, poderá usar os seguintes comandos:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

Neste momento, o SQL Server está em execução no seu computador RHEL e está pronto para uso!

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="install-sql-server"></a><a id="install"></a>Instalar o SQL Server

> [!NOTE]
> Os seguintes comandos do SQL Server 2019 apontam para o repositório do RHEL 8. O RHEL 8 não vem pré-instalado com o Python 2, que é exigido pelo SQL Server. Antes de começar as etapas de instalação do SQL Server, execute o comando e verifique se python2 está selecionado como o interpretador: 
>
> ```
> sudo alternatives --config python
> # If not configured, install python2 and openssl10 using the following commands: 
> sudo yum install python2
> sudo yum install compat-openssl10
> # Configure python2 as the default interpreter using this command: 
> sudo alternatives --config python
> ``` 
> Para obter mais informações sobre essas etapas, confira o seguinte blog sobre como instalar o python2 e configurá-lo como o interpretador padrão: https://www.redhat.com/en/blog/installing-microsoft-sql-server-red-hat-enterprise-linux-8-beta.
> 
> Se você estiver usando o RHEL 7, altere o caminho abaixo para `/rhel/7` em vez de `/rhel/8`.

Para configurar o SQL Server no RHEL, execute os seguintes comandos em um terminal para instalar o pacote **mssql-server**:

1. Baixe o arquivo de configuração do repositório do Red Hat do Microsoft SQL Server 2019:

   ```bash
   sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/8/mssql-server-2019.repo
   ```

2. Execute os comandos a seguir para instalar o SQL Server:

   ```bash
   sudo yum install -y mssql-server
   ```

3. Após a conclusão da instalação do pacote, execute a **instalação de mssql-conf** e siga os prompts para definir a senha SA e escolher sua edição.

   ```bash
   sudo /opt/mssql/bin/mssql-conf setup
   ```

   > [!NOTE]
   > Especifique uma senha forte para a conta SA (comprimento mínimo de 8 caracteres, incluindo letras maiúsculas e minúsculas, 10 dígitos básicos e/ou símbolos não alfanuméricos).

4. Após concluir a configuração, verifique se o serviço está em execução:

   ```bash
   systemctl status mssql-server
   ```

5. Para permitir conexões remotas, abra a porta do SQL Server no firewall no RHEL. A porta do SQL Server padrão é TCP 1433. Se você estiver usando **FirewallD** para o firewall, poderá usar os seguintes comandos:

   ```bash
   sudo firewall-cmd --zone=public --add-port=1433/tcp --permanent
   sudo firewall-cmd --reload
   ```

Neste momento, o SQL Server 2019 está em execução no seu computador RHEL e está pronto para uso!

::: moniker-end

## <a name="install-the-sql-server-command-line-tools"></a><a id="tools"></a>Instalar as ferramentas de linha de comando do SQL Server

Para criar um banco de dados, é necessário conectar-se a uma ferramenta que pode executar instruções Transact-SQL no SQL Server. As seguintes etapas instalam as ferramentas de linha de comando do SQL Server: [sqlcmd](../tools/sqlcmd-utility.md) e [bcp](../tools/bcp-utility.md).

1. Baixe o arquivo de configuração do repositório do Red Hat da Microsoft.

   ```bash
   sudo curl -o /etc/yum.repos.d/msprod.repo https://packages.microsoft.com/config/rhel/8/prod.repo
   ```

1. Se você tiver uma versão anterior do **mssql-tools** instalada, remova os pacotes unixODBC mais antigos.

   ```bash
   sudo yum remove unixODBC-utf16 unixODBC-utf16-devel
   ```

1. Execute os seguintes comandos para instalar **mssql-tools** com o pacote do desenvolvedor do unixODBC. Para obter mais informações, confira [Instalar o Microsoft ODBC Driver for SQL Server (Linux)](../connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md).

   ```bash
   sudo yum install -y mssql-tools unixODBC-devel
   ```

1. Para sua conveniência, adicione `/opt/mssql-tools/bin/` à sua variável de ambiente **PATH**. Isso permite que você execute as ferramentas sem especificar o caminho completo. Execute os seguintes comandos para modificar o **PATH** para sessões de logon e sessões interativas/que não são de logon:

   ```bash
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bash_profile
   echo 'export PATH="$PATH:/opt/mssql-tools/bin"' >> ~/.bashrc
   source ~/.bashrc
   ```

[!INCLUDE [Connect, create, and query data](../includes/sql-linux-quickstart-connect-query.md)]
