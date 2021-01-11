---
title: Instalar um runtime personalizado de Python
description: Saiba como instalar um runtime personalizado do Python para o SQL Server usando Extensões de Linguagem. O runtime personalizado do Python pode ser usado para machine learning.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/30/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
zone_pivot_groups: python-custom-runtime-platform
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 91aace4333b4496338b782344e64cdfea2b886bd
ms.sourcegitcommit: 5b2c47ce88f7e56552fd415c32b319009d043b56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97804320"
---
# <a name="install-a-python-custom-runtime-for-sql-server"></a>Instalar um runtime personalizado de Python para o SQL Server
[!INCLUDE [SQL Server 2019 and later](../../includes/applies-to-version/sqlserver2019.md)]

Este artigo descreve como instalar um runtime personalizado do Python para executar scripts externos do Python com o SQL Server. O runtime personalizado usa as [Extensões de Linguagem do SQL Server](../../language-extensions/language-extensions-overview.md) e pode ser usado para executar scripts de machine learning.

O runtime personalizado do Python permite que você use sua versão do runtime do Python com o SQL Server, em vez da versão de runtime padrão instalada com os [Serviços de Machine Learning do SQL Server](../sql-server-machine-learning-services.md).

::: zone pivot="python-custom-runtime-windows"

## <a name="prerequisites"></a>Pré-requisitos

Antes de instalar um runtime personalizado de Python, instale o seguinte:

+ Instale a [CU (atualização cumulativa) 3 ou posterior](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md) do SQL Server 2019.

+ Instale o [Python 3.7](https://www.python.org/downloads/) no servidor.

    Atualmente, a extensão de linguagem do Python usada para o runtime personalizado do Python só dá suporte ao Python 3.7. Caso deseje usar uma versão diferente do Python, siga a instrução descrita no [repositório GitHub da Extensão de Linguagem do Python](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/python) para modificar e recompilar a extensão.

    > [!IMPORTANT]
    > Durante a instalação do Python, marque **Adicionar Python 3.7 ao PATH**.

## <a name="install-language-extensions"></a>Instalar extensões de linguagem

> [!NOTE]
> Se você tem os [Serviços de Machine Learning instalados](../sql-server-machine-learning-services.md) no SQL Server 2019, as Extensões de Linguagem já estão instaladas e você pode ignorar esta etapa.

Siga as etapas abaixo para instalar as [Extensões de Linguagem do SQL Server](../../language-extensions/language-extensions-overview.md), que são usadas para o runtime personalizado do Python.

1. Inicie o assistente de instalação do SQL Server 2019.
  
1. Na guia **Instalação**, selecione **Nova instalação autônoma do SQL Server ou adicionar recursos a uma instalação existente**.

1. Na página **Seleção de Recursos** , selecione estas opções:
  
    + **Serviços do Mecanismo de Banco de Dados**
  
        Para usar as Extensões de Linguagem com o SQL Server, você deverá instalar uma instância do mecanismo de banco de dados. Use uma instância nova ou existente.
  
    + **Serviços de Machine Learning e Extensões de Linguagem**

        Selecione **Serviços de Machine Learning e Extensões de Linguagem**. Não selecione Python, pois você instalará o runtime do Python personalizado mais tarde.

        :::image type="content" source="media/2019-setup-language-extensions.png" alt-text="Instalação das Extensões de Linguagem do SQL Server 2019.":::

1. Na página **Pronto para instalar**, verifique se essas seleções estão incluídas e selecione **Instalar**.
  
    + Serviços do Mecanismo de Banco de Dados
    + Serviços de Machine Learning e Extensões de Linguagem

1. Após a conclusão da instalação, reinicie o computador, se solicitado.

> [!IMPORTANT]
> Se você instalar uma nova instância do SQL Server 2019 com as Extensões de Linguagem, instale a [CU (atualização cumulativa) 3 ou posterior](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md) antes de prosseguir para a próxima etapa.

## <a name="install-pandas"></a>Instalar o pandas

Instale o pacote [pandas](https://pandas.pydata.org/) para Python em um prompt de comandos *com privilégios elevados*:

```bash
python.exe -m pip install pandas
```

## <a name="add-environment-variable"></a>Adicionar uma variável de ambiente

Adicione ou modifique a variável de ambiente do sistema **PYTHONHOME**.

1. Na caixa de pesquisa do Windows, digite *ambiente* e selecione **Editar as variáveis de ambiente do sistema**.
1. Na guia **Avançado**, selecione **Variáveis de Ambiente**.
1. Em **Variáveis do sistema**, selecione **Novo** para criar **PYTHONHOME** de modo que ele aponte para a localização de instalação do Python 3.7. Se PYTHONHOME já existir, selecione **Editar** para apontar para o local de instalação do Python 3.7.
1. Selecione **OK** para fechar todas as janelas.

    :::image type="content" source="media/pythonhome-env-variable.png" alt-text="Variável de ambiente PYTHONHOME.":::

## <a name="grant-access-to-python-folder"></a>Permitir acesso à pasta do Python

Execute os comandos **icacls** a seguir em um novo prompt de comandos *com privilégios elevados* para permitir o acesso de **LEITURA E EXECUÇÃO** a **PYTHONHOME** ao **Serviço SQL Server Launchpad** e ao SID **S-1-15-2-1** (**ALL_APPLICATION_PACKAGES**).

1. Conceder permissões ao **Nome de usuário do Serviço SQL Server Launchpad**.

    ```cmd
    icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD":(OI)(CI)RX /T
    ```

    Para a instância nomeada, o comando será `icacls "%PYTHONHOME%" /grant "NT Service\MSSQLLAUNCHPAD$SQL01":(OI)(CI)RX /T` para uma instância chamada **SQL01**.

2. Conceda permissões a **SID S-1-15-2-1**.

    ```cmd
    icacls "%PYTHONHOME%" /grant *S-1-15-2-1:(OI)(CI)RX /T
    ```

    O comando anterior concede permissões ao SID **S-1-15-2-1** do computador, que é equivalente a **TODOS OS PACOTES DE APLICATIVOS** em uma versão em inglês do Windows. Como alternativa, é possível usar `icacls "%R_HOME%" /grant "ALL APPLICATION PACKAGES":(OI)(CI)RX /T` em uma versão em inglês do Windows.

## <a name="restart-sql-server-launchpad"></a>Reiniciar o SQL Server Launchpad

Siga estas etapas para reiniciar o serviço SQL Server Launchpad.

1. Abra o [SQL Server Configuration Manager](../../relational-databases/sql-server-configuration-manager.md).

1. Em **Serviços do SQL Server**, clique com o botão direito do mouse em **SQL Server Launchpad (MSSQLSERVER)** e selecione **Reiniciar**. Se estiver usando uma instância nomeada, o nome da instância será mostrado em vez de **(MSSQLSERVER)** .

## <a name="register-language-extension"></a>Registrar a extensão de linguagem

Siga estas etapas para baixar e registrar a extensão de linguagem do Python, que é usada para o runtime personalizado do Python.

1. Baixe o arquivo **python-lang-extension-windows.zip** do [repositório GitHub das Extensões de Linguagem do SQL Server](https://github.com/microsoft/sql-server-language-extensions/releases).

    Como alternativa, você pode usar a versão de depuração (**python-lang-extension-windows-debug.zip**) em um ambiente de desenvolvimento ou teste. A versão de depuração fornece informações detalhadas de log para investigar os erros e não é recomendada para ambientes de produção.

1. Use o [Azure Data Studio](../../azure-data-studio/what-is-azure-data-studio.md) para se conectar à sua instância do SQL Server e execute o comando T-SQL a seguir para registrar a extensão de linguagem do Python com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md). 

    Modifique o caminho na instrução de maneira a refletir a localização do arquivo zip da extensão de linguagem baixada (**python-lang-extension-windows.zip**).

    ```sql
    CREATE EXTERNAL LANGUAGE [myPython]
    FROM (CONTENT = N'/path/to/python-lang-extension-windows.zip', FILE_NAME = 'pythonextension.dll');
    GO
    ```

    Execute a instrução para cada banco de dados no qual deseja usar a extensão de linguagem do Python.

    > [!NOTE]
    > **Python** é uma palavra reservada e não pode ser usada como o nome de uma nova linguagem externa. Use outro nome. Por exemplo, a instrução acima usa **myPython**.

::: zone-end

::: zone pivot="python-custom-runtime-linux"

## <a name="prerequisites"></a>Pré-requisitos

Antes de instalar um runtime personalizado de Python, instale o seguinte:

+ Instale o SQL Server 2019 para Linux. Você pode instalar o SQL Server no Red Hat Enterprise Linux (RHEL), no SUSE Linux Enterprise Server (SLES) e no Ubuntu. Para obter mais informações, confira [as diretrizes de instalação do SQL Server em Linux](../../linux/sql-server-linux-setup.md).

+ Faça a atualização para a CU (atualização cumulativa) 3 ou posterior do SQL Server 2019. Siga estas etapas:
    1. Configure os repositórios para atualizações cumulativas. Para obter mais informações, confira [Configurar repositórios para instalar e atualizar o SQL Server em Linux](../../linux/sql-server-linux-change-repo.md).

    1. Atualize o pacote **mssql-server** para a atualização cumulativa mais recente. Para obter mais informações, confira [a seção Atualizar o SQL Server nas diretrizes de instalação do SQL Server em Linux](../../linux/sql-server-linux-setup.md#upgrade).

+ Instale o [Python 3.7](https://www.python.org/downloads/) no servidor.

    Atualmente, a extensão de linguagem do Python usada para o runtime personalizado do Python só dá suporte ao Python 3.7. Caso deseje usar uma versão diferente do Python, siga a instrução descrita no [repositório GitHub da Extensão de Linguagem do Python](https://github.com/microsoft/sql-server-language-extensions/tree/master/language-extensions/python) para modificar e recompilar a extensão.

## <a name="install-language-extensions"></a>Instalar extensões de linguagem

> [!NOTE]
> Se você tem os [Serviços de Machine Learning](../sql-server-machine-learning-services.md) instalados no SQL Server 2019, o pacote **mssql-server-extensibility** de Extensões de Linguagem já está instalado e você pode ignorar esta etapa.

Siga os comandos abaixo para instalar as [Extensões de Linguagem do SQL Server](../../language-extensions/language-extensions-overview.md) no Linux, que são usadas para o runtime personalizado do Python.

#### <a name="ubuntu"></a>[Ubuntu](#tab/ubuntu)

1. Se possível, execute este comando para atualizar os pacotes no sistema antes da instalação.

    ```bash
    # Install as root or sudo
    sudo apt-get update
    ```

1. O Ubuntu pode não ter a opção de transporte https apt. Para instalá-lo, execute este comando.

    ```bash
    # Install as root or sudo
    apt-get install apt-transport-https
    ```

1. Instale **mssql-server-extensibility** com este comando.

    ```bash
    # Install as root or sudo
    sudo apt-get install mssql-server-extensibility
    ```

#### <a name="red-hat-enterprise-linux-rhel"></a>[Red Hat Enterprise Linux (RHEL)](#tab/rhel)

```bash
# Install as root or sudo
sudo yum install mssql-server-extensibility
```

#### <a name="suse-linux-enterprise-server-sles"></a>[SUSE Linux Enterprise Server (SLES)](#tab/sles)

```bash
# Install as root or sudo
sudo zypper install mssql-server-extensibility
```

---

## <a name="install-python-37-and-pandas"></a>Instalar Python 3.7 e pandas

Instale o Python 3.7, a biblioteca libpython3.7 e o pacote pandas. 

Os seguintes comandos são exemplo para o Ubuntu:

```bash
# Install python3.7 and the corresponding library:
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt-get update
sudo apt-get install python3.7 python3-pip libpython3.7

# Install pandas to /usr/lib:
sudo python3.7 -m pip install pandas -t /usr/lib/python3.7/dist-packages
```

## <a name="custom-installation-of-python"></a>Instalação personalizada do Python

> [!NOTE]
> Se você instalou o Python 3.7 na localização padrão `/usr/lib/python3.7`, ignore esta seção e passe para a seção [Registrar a extensão de linguagem](#register-language-extension-linux).

Se você criou sua versão do Python 3.7, use os comandos a seguir para permitir que o SQL Server reconheça sua instalação personalizada.

### <a name="add-environment-variable"></a>Adicionar uma variável de ambiente

Primeiro, edite o serviço **mssql-launchpadd** para adicionar a variável de ambiente **PYTHONHOME** ao arquivo `/etc/systemd/system/mssql-launchpadd.service.d/override.conf`

1. Abra o arquivo com o systemctl

    ```bash
    sudo systemctl edit mssql-launchpadd
    ```

1. Insira o texto a seguir no arquivo `/etc/systemd/system/mssql-launchpadd.service.d/override.conf` que é aberto. Defina o valor de **PYTHONHOME** como o caminho de instalação personalizada do Python.

    ```
    [Service]
    Environment="PYTHONHOME=/path/to/installation/of/python3.7"
    ```

1. Salve o arquivo e feche o editor.

Depois, verifique se `libpython3.7m.so.1.0` pode ser carregado.

1. Crie um arquivo custom-python.conf em `/etc/ld.so.conf.d`.

    ```bash
    sudo vi /etc/ld.so.conf.d/custom-python.conf
    ```

1. No arquivo que é aberto, adicione o caminho para **libpython3.7m.so.1.0** da instalação personalizada do Python.

    ```
    /path/to/installation/of/python3.7/lib
    ```

1. Salve o novo arquivo e feche o editor.

1. Execute `ldconfig` e verifique se `libpython3.7m.so.1.0` pode ser carregado executando os comandos a seguir e verificando se todas as bibliotecas dependentes podem ser encontradas.

    ```bash
    sudo ldconfig
    ldd /path/to/installation/of/python3.7/lib/libpython3.7m.so.1.0
    ```

### <a name="grant-access-to-python-folder"></a>Permitir acesso à pasta do Python

Defina a opção `datadirectories` na seção de extensibilidade do arquivo /var/opt/mssql/mssql.conf como a instalação personalizada de Python.

```bash
sudo /opt/mssql/bin/mssql-conf set extensibility.datadirectories /path/to/installation/of/python3.7
```

### <a name="restart-mssql-launchpadd"></a>Reiniciar o mssql-launchpadd

```bash
sudo systemctl restart mssql-launchpadd
```

<a name="register-language-extension-linux"></a>

## <a name="register-language-extension"></a>Registrar a extensão de linguagem

Siga estas etapas para baixar e registrar a extensão de linguagem do Python, que é usada para o runtime personalizado do Python.

1. Baixe o arquivo **python-lang-extension-linux.zip** do [repositório GitHub das Extensões de Linguagem do SQL Server](https://github.com/microsoft/sql-server-language-extensions/releases).

    Como alternativa, você pode usar a versão de depuração (**python-lang-extension-linux-debug.zip**) em um ambiente de desenvolvimento ou teste. A versão de depuração fornece informações detalhadas de log para investigar os erros e não é recomendada para ambientes de produção.

1. Use o [Azure Data Studio](../../azure-data-studio/what-is-azure-data-studio.md) para se conectar à sua instância do SQL Server e execute o comando T-SQL a seguir para registrar a extensão de linguagem do Python com [CREATE EXTERNAL LANGUAGE](../../t-sql/statements/create-external-language-transact-sql.md). 

    Modifique o caminho na instrução de maneira a refletir a localização do arquivo zip da extensão de linguagem baixada (**python-lang-extension-linux.zip**).

    ```sql
    CREATE EXTERNAL LANGUAGE [myPython]
    FROM (CONTENT = N'/path/to/python-lang-extension-linux.zip', FILE_NAME = 'libPythonExtension.so.1.0');
    GO
    ```

    Execute a instrução para cada banco de dados no qual deseja usar a extensão de linguagem do Python.

    > [!NOTE]
    > **Python** é uma palavra reservada e não pode ser usada como o nome de uma nova linguagem externa. Use outro nome. Por exemplo, a instrução acima usa **myPython**.

::: zone-end

## <a name="enable-external-script"></a>Habilitar um script externo

Você pode executar um script externo do Python com o procedimento armazenado [sp_execute_external script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md).

Para habilitar scripts externos, use o [Azure Data Studio](../../azure-data-studio/what-is-azure-data-studio.md) para executar a instrução abaixo.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE;  
```

## <a name="verify-installation"></a>Verifique a instalação

Use o script SQL a seguir para verificar a instalação e a funcionalidade do runtime personalizado do Python.

```sql
EXEC sp_execute_external_script
@language =N'myPython',
@script=N'
import sys
print(sys.path)
print(sys.version)
print(sys.executable)'
```

## <a name="next-steps"></a>Próximas etapas

+ [Instalar um runtime personalizado de R para o SQL Server](custom-runtime-r.md)
+ [Estrutura de extensibilidade no SQL Server](../concepts/extensibility-framework.md)
+ [Visão geral das Extensões de Linguagem](../../language-extensions/language-extensions-overview.md)
