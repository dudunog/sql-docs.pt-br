---
title: Baixar o SQL Server Management Studio (SSMS)
description: Baixe a versão mais recente do SSMS (SQL Server Management Studio).
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
keywords:
- instalar ssms, baixar ssms, ssms mais recentes
- SQL Server Management Studio
- ssms.exe
- sql man studio
- sql management studio
- instalação do SQL management studio
- baixar o sql management studio
- ms sql management studio
- instalar o sql management studio
- ssms download
- sql server ssms
- ssms express
ms.assetid: adafeeef-4255-4924-8042-02f503d599ca
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan
ms.custom: seo-lt-2019
ms.date: 12/17/2020
ms.openlocfilehash: a4798fbc01e015b85e31d9768fd8135af6d202f4
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596876"
---
# <a name="download-sql-server-management-studio-ssms"></a>Baixar o SQL Server Management Studio (SSMS)

[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

O SSMS (SQL Server Management Studio) é um ambiente integrado para gerenciar qualquer infraestrutura de SQL, do SQL Server para o Banco de Dados SQL do Azure. O SSMS fornece ferramentas para configurar, monitorar e administrar instâncias do SQL Server e bancos de dados. Use o SSMS para implantar, monitorar e atualizar os componentes da camada de dados usados pelos seus aplicativos, além de criar consultas e scripts.

Use o SSMS para consultar, criar e gerenciar seus bancos de dados e data warehouses, independentemente de onde estiverem – no computador local ou na nuvem.

## <a name="download-ssms"></a>Baixar o SSMS

:::image type="icon" source="media/download-icon.png" border="false"::: **[Baixar o SQL Server Management Studio (SSMS)](https://aka.ms/ssmsfullsetup)**

O SSMS 18.8 é a versão em GA (disponibilidade geral) mais recente do SSMS. Se você tiver uma versão anterior em GA do SSMS 18 instalada, a instalação do SSMS 18.8 atualizará o produto para a versão 18.8.

[!INCLUDE [ssms-ads-install](../includes/ssms-azure-data-studio-install.md)]

- Número da versão: 18.8
- Número de build: 15.0.18369.0
- Data de lançamento: 17 de dezembro de 2020

Se você tem sugestões, comentários ou deseja relatar problemas, a melhor maneira de entrar em contato com a equipe do SSMS é usando os [comentários do usuário do SQL Server](https://aka.ms/sqlfeedback).

A instalação do SSMS 18.x não atualiza nem substitui versões do SSMS 17.x ou anteriores. O SSMS 18.x é instalado lado a lado com versões anteriores para que as duas versões estejam disponíveis para uso. No entanto, se você tiver uma *versão prévia* do SSMS 18.x instalada, precisará desinstalá-la antes de instalar o SSMS 18.8. Para conferir se você tem a versão prévia, acesse a janela **Ajuda > Sobre**.

Se um computador contiver instalações lado a lado do SSMS, verifique se você iniciou a versão correta para suas necessidades específicas. A versão mais recente é rotulada **Microsoft SQL Server Management Studio 18**

> [!Note]
> Se você estiver acessando esta página em uma versão de idioma diferente do inglês e desejar ver o conteúdo mais atualizado, acesse a [versão do site em inglês dos EUA](). Você pode baixar idiomas diferentes do site da versão em inglês dos EUA selecionando [idiomas disponíveis](#available-languages).

## <a name="available-languages"></a>Idiomas disponíveis

Esta versão do SSMS pode ser instalada nos seguintes idiomas:

SQL Server Management Studio 18.8:  
[Chinês (Simplificado)](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x804) | [Chinês (Tradicional)](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x404) | [Inglês (Estados Unidos)](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x409) | [Francês](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x40c) | [Alemão](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x407) | [Italiano](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x410) | [Japonês](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x411) | [Coreano](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x412) | [Português (Brasil)](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x416) | [Russo](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x419) | [Espanhol](https://go.microsoft.com/fwlink/?linkid=2151644&clcid=0x40a)

> [!NOTE]
> O módulo do SQL Server PowerShell é uma instalação separada por meio da Galeria do PowerShell. Para obter mais informações, consulte [Baixar o Módulo SQL Server PowerShell](../powershell/download-sql-server-ps-module.md).

## <a name="whats-new"></a>Novidades

Para obter detalhes e mais informações sobre as novidades desta versão, confira as [Notas sobre a versão do SSMS](release-notes-ssms.md).

Há alguns [problemas conhecidos](release-notes-ssms.md#known-issues-188) nesta versão.

## <a name="previous-versions"></a>Versões anteriores

Este artigo destina-se somente à versão mais recente do SSMS. Para baixar as versões anteriores do SSMS, acesse [Versões anteriores do SSMS](../ssms/release-notes-ssms.md#previous-ssms-releases).

[!INCLUDE[ssms-connect-azure-ad](../includes/ssms-connect-azure-ad.md)]

## <a name="unattended-install"></a>Instalação autônoma

Você também pode instalar o SSMS usando um script de prompt de comando.

Se quiser instalar o SSMS em segundo plano sem prompts de GUI, siga as etapas abaixo.

1. Inicialize o prompt de comando com permissões elevadas.

2. Digite o comando abaixo no prompt de comando.

    ```console
    start "" /w <path where SSMS-ENU.exe file is located> /Quiet SSMSInstallRoot=<path where you want to install SSMS>
    ```

    Exemplo:

    ```console
    start "" /w %systemdrive%\SSMSfrom\SSMS-Setup-ENU.exe /Quiet SSMSInstallRoot=%systemdrive%\SSMSto
    ```

    Você também pode passar */Passive* em vez de */Quiet* para ver a interface do usuário da configuração.

3. Se tudo correr bem, será possível ver o SSMS instalado em %systemdrive%\SSMSto\Common7\IDE\Ssms.exe" com base no exemplo. Se algo der errado, você poderá inspecionar o código de erro retornado e dar uma olhada em %TEMP%\SSMSSetup para o arquivo de log.

## <a name="installation-with-azure-data-studio"></a>Instalação com o Azure Data Studio

- A partir do SSMS 18.7, o SSMS instala uma versão de sistema do Azure Data Studio por padrão.  Se já houver na estação de trabalho uma versão de sistema do Azure Data Studio estável ou insiders igual ou superior à versão incluída do Azure Data Studio, a instalação dele pelo SSMS será ignorada. A versão do Azure Data Studio pode ser encontrada nas notas de versão.
- O instalador do sistema Azure Data Studio requer os mesmos direitos de segurança que o instalador do SSMS.
- A instalação do Azure Data Studio é concluída com as opções de instalação padrão. Uma pasta do menu Iniciar é criada, e o Azure Data Studio é adicionado a PATH. Um atalho de área de trabalho não é criado, e o Azure Data Studio não é registrado como um editor padrão para nenhum tipo de arquivo.
- A localização do Azure Data Studio é realizada por meio de extensões do Pacote de Idiomas. Para localizar o Azure Data Studio, baixe o pacote de idiomas correspondente do [marketplace de extensões](../azure-data-studio/extensions/add-extensions.md).
- No momento, a instalação do Azure Data Studio pode ser ignorada iniciando o instalador do SSMS com o sinalizador de linha de comando `DoNotInstallAzureDataStudio=1`.

## <a name="uninstall"></a>Desinstalar

Há componentes compartilhados que permanecem instalados após a desinstalação do SSMS.

Esses componentes são:

- Azure Data Studio
- Microsoft .NET Framework 4.7.2
- Driver do Microsoft OLE DB para SQL Server
- Microsoft ODBC Driver 17 for SQL Server
- Pacote Redistribuível do Microsoft Visual C++ 2013 (x86)
- Pacote Redistribuível do Microsoft Visual C++ 2017 (x86)
- Pacote Redistribuível do Microsoft Visual C++ 2017 (x64)
- Microsoft Visual Studio Tools for Applications 2017

Esses componentes não são desinstalados porque eles podem ser compartilhados com outros produtos. Se estiverem desinstalados, você corre o risco de desabilitar outros produtos.

## <a name="supported-sql-offerings"></a>Ofertas de SQL com suporte

- Esta versão do SSMS funciona com todas as [versões com suporte do SQL Server 2008 – [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]](https://support.microsoft.com/lifecycle?C2=1044) e fornece o maior nível de suporte para trabalhar com os recursos de nuvem mais recentes no Banco de Dados SQL do Azure e Azure Synapse Analytics.
- Além disso, o SSMS 18.x pode ser instalado lado a lado com o SSMS 17.x, o SSMS 16.x ou o SSMS do SQL Server 2014 e anteriores.
- SSIS (SQL Server Integration Services) – a versão SSMS 17.x ou posterior não dá suporte à conexão com o serviço herdado do SQL Server Integration Services. Para conectar-se a uma versão anterior do Integration Services herdado, use a versão do SSMS alinhada com a versão do SQL Server. Por exemplo, use o SSMS 16.x para conectar ao serviço herdado do SQL Server Integration Services 2016. O SSMS 17.x e o 16.x podem ser instalados lado a lado no mesmo computador. Desde o lançamento do SQL Server 2012, o banco de dados de catálogo do SSIS, o SSISDB, é a maneira recomendada para armazenar, gerenciar, executar e monitorar os pacotes do Integration Services. Para obter detalhes, veja o [Catálogo do SSIS](../integration-services/catalog/ssis-catalog.md).

## <a name="ssms-system-requirements"></a>Requisitos do Sistema do SSMS

A versão atual do SSMS dá suporte às seguintes plataformas de 64 bits quando usadas com o service pack mais atual disponível:

Sistemas operacionais com suporte:

- Windows 10 (64 bits) versão 1607 (10.0.14393) ou posterior
- Windows 8.1 (64 bits)
- Windows Server 2019 (64 bits)
- Windows Server 2016 (64 bits)
- Windows Server 2012 R2 (64 bits)
- Windows Server 2012 (64 bits)
- Windows Server 2008 R2 (64 bits)

Hardware com suporte:

- Processador (Intel, AMD) x86 de 1,8 GHz ou mais rápido. Núcleo duplo ou superior recomendado
- 2 GB de RAM; 4 GB de RAM são recomendados (mínimo de 2,5 GB se executado em uma máquina virtual)
- Espaço em disco rígido: Mínimo de 2 GB e máximo de 10 GB de espaço disponível

> [!NOTE]
> O SSMS está disponível apenas como um aplicativo de 32 bits para Windows. Se você precisa de uma ferramenta que seja executada em sistemas operacionais diferentes do Windows, recomendamos o Azure Data Studio. O Azure Data Studio é uma ferramenta multiplataforma executada no macOS, no Linux e no Windows. Para obter detalhes, veja [Azure Data Studio](../azure-data-studio/what-is-azure-data-studio.md).

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

## <a name="next-steps"></a>Próximas etapas

- [Ferramentas do SQL](../tools/overview-sql-tools.md)
- [Documentação do SQL Server Management Studio](sql-server-management-studio-ssms.md)
- [Azure Data Studio](../azure-data-studio/what-is-azure-data-studio.md)
- [Baixar o SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- [Atualizações mais recentes](../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)
- [Guia de Arquitetura de Dados do Azure](/azure/architecture/data-guide/)
- [Blog do SQL Server](https://cloudblogs.microsoft.com/sqlserver/)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]