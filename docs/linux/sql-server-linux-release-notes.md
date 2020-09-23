---
title: Notas sobre a versão do SQL Server 2017 em Linux
description: Este artigo contém as notas sobre a versão e os recursos com suporte do SQL Server 2017 em execução no Linux. As notas sobre a versão aqui incluídas são para a versão mais recente, bem como para diversas versões anteriores.
author: VanMSFT
ms.author: vanto
ms.date: 09/10/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1314744f-fcaf-46db-800e-2918fa7e1b6c
ms.openlocfilehash: dd0473eea265df700c1224ba4db8edf2dbff9e9e
ms.sourcegitcommit: 49706fb7efb46ee467e88dc794a1eab916a9af25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90013669"
---
# <a name="release-notes-for-sql-server-2017-on-linux"></a>Notas sobre a versão do SQL Server 2017 em Linux

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

As notas sobre a versão a seguir se aplicam ao [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] em execução no Linux. Este artigo está dividido em seções para cada versão. A versão de GA tem o suporte detalhado e os problemas conhecidos listados. Cada CU (atualização cumulativa) ou GDR (versão de distribuição geral ) tem um link para um artigo de suporte que descreve as alterações da atualização cumulativa, bem como links para os downloads dos pacotes do Linux.

> [!TIP]
> Essas notas sobre a versão são referentes especificamente às versões do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. Para obter mais informações sobre o novo [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)], confira [Notas sobre a versão prévia do SQL Server 2019 em Linux](sql-server-linux-release-notes-2019.md?view=sql-server-ver15&preserve-view=true).

## <a name="supported-platforms"></a>Plataformas compatíveis

| Plataforma | Sistema de Arquivos | Guia de Instalação |
|-----|-----|-----|
| Red Hat Enterprise Linux 7.3, 7.4, 7.5, 7.6 ou 8 Server | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-red-hat.md) | 
| SUSE Enterprise Linux Server v12 SP2 | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-suse.md) |
| Ubuntu 16.04 LTS, 18.04 LTS | XFS ou EXT4 | [Guia de instalação](quickstart-install-connect-ubuntu.md) | 
| Docker Engine 1.8+ no Windows, Mac ou Linux | N/D | [Guia de instalação](quickstart-install-connect-docker.md) | 

> [!TIP]
> Para obter mais informações, examine os [requisitos do sistema](sql-server-linux-setup.md#system) para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Linux. Para obter a política de suporte mais recente para [!INCLUDE[ssSQL17](../includes/sssql17-md.md)], confira a [Política de suporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

## <a name="tools"></a>Ferramentas

A maioria das ferramentas de cliente existentes que se destinam ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode se direcionar diretamente ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em execução no Linux. Algumas ferramentas podem ter um requisito de versão específico para funcionar bem com o Linux. Para obter uma lista completa de ferramentas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], confira [Ferramentas e utilitários de SQL para SQL Server](../tools/overview-sql-tools.md).

## <a name="release-history"></a>Histórico de versões

A tabela a seguir lista o histórico de versões do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].

| Versão               | Versão       | Data de liberação |
|-----------------------|---------------|--------------|
| [CU22](#CU22)         | 14.0.3356.20  | 2020-09-10   |
| [CU21](#CU21)         | 14.0.3335.7   | 2020-07-01   |
| [CU20](#CU20)         | 14.0.3294.2   | 10-04-2020   |
| [CU19](#CU19)         | 14.0.3281.6   | 2020-02-05   |
| [CU18](#CU18)         | 14.0.3257.3   | 09/12/2019   |
| [CU17](#CU17)         | 14.0.3238.1   | 08-10-2019   |
| [CU16](#CU16)         | 14.0.3223.3   | 01-08-2019   |
| [CU15](#CU15)         | 14.0.3162.1   | 23-05-2019   |
| [CU14](#CU14)         | 14.0.3076.1   | 25-03-2019   |
| [CU13](#CU13)         | 14.0.3048.4   | 18-12-2018   |
| [CU12](#CU12)         | 14.0.3045.24  | 24-10-2018   |
| [CU11](#CU11)         | 14.0.3038.14  | 20-09-2018   |
| [CU10](#CU10)         | 14.0.3037.1   | 27-08-2018   |
| [CU9-GDR2](#CU9-GDR2) | 14.0.3035.2   | 18-08-2018   |
| [GDR2](#GDR2)         | 14.0.2002.14  | 18-08-2018   |
| [CU9](#CU9)           | 14.0.3030.27  | 18-07-2018   |
| [CU8](#CU8)           | 14.0.3029.16  | 21-06-2018   |
| [CU7](#CU7)           | 14.0.3026.27  | 24-05-2018   |
| [CU6](#CU6)           | 14.0.3025.34  | 19-04-2018   |
| [CU5](#CU5)           | 14.0.3023.8   | 20-03-2018   |
| [CU4](#CU4)           | 14.0.3022.28  | 20-02-2018   |
| [CU3](#CU3)           | 14.0.3015.40  | 03-01-2018   |
| [GDR1](#GDR1)         | 14.0.2000.63  | 03-01-2018   |
| [CU2](#CU2)           | 14.0.3008.27  | 28-11-2017   |
| [CU1](#CU1)           | 14.0.3006.16  | 24-10-2017   |
| [GA](#GA)             | 14.0.1000.169 | 02-10-2017   |

## <a name="how-to-install-updates"></a><a id="cuinstall"></a> Como instalar atualizações

Se tiver configurado o repositório da CU (**mssql-server-2017**), você obterá os pacotes mais recentes da CU do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] quando executar novas instalações. O repositório da CU é padrão para todos os artigos de instalação de pacotes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Linux. Se tiver configurado o repositório GDR (**mssql-server-2017-gdr**), você só obterá atualizações de segurança críticas lançadas desde a GA. Se você precisar de atualizações da CU ou da GDR do contêiner do Docker, veja as imagens oficiais para [Microsoft SQL Server em Linux para Docker Engine](https://hub.docker.com/r/microsoft/mssql-server). Para obter mais informações sobre a configuração do repositório, confira [Configurar repositórios para SQL Server em Linux](sql-server-linux-change-repo.md).

Se você estiver atualizando pacotes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] existentes, execute o comando de atualização adequado para cada pacote a fim de obter a atualização cumulativa mais recente. Para obter instruções de atualização específicas para cada pacote, confira os seguintes guias de instalação:

- [Instalar pacote do SQL Server](sql-server-linux-setup.md#upgrade)
- [Instalar pacote de Pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)
- [Habilitar o SQL Server Agent](sql-server-linux-setup-sql-agent.md)

## <a name="cu22-september-2020"></a><a id="CU22"></a> CU22 (setembro de 2020)

Esta é a versão da Atualização Cumulativa 22 (CU22) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] dela é 14.0.3356.20. Para obter informações sobre as correções e aprimoramentos nesta versão, confira <https://support.microsoft.com/help/4577467>.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

> [!NOTE]
> O **Ubuntu 18.04** e o **RHEL 8** agora são compatíveis com o SQL Server 2017 a partir da CU20.
>
> Os links de instalação do pacote offline do Ubuntu apontam para os pacotes do Ubuntu 18.04, exceto para o pacote SSIS (que não está disponível para o Ubuntu 18.04). Se você estiver procurando pacotes do Ubuntu 16.04, confira o caminho para baixar <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/>.
>
> Os links de instalação do pacote offline do Red Hat apontam para os pacotes do RHEL 8, exceto para o pacote SSIS (que não está disponível para o RHEL 8). Se você estiver procurando pacotes do RHEL 7, confira o caminho para baixar <https://packages.microsoft.com/rhel/7/mssql-server-2017/>.

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3356.20-23 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-14.0.3356.20-23.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-ha-14.0.3356.20-23.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-fts-14.0.3356.20-23.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3356.20-23 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3356.20-23.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3356.20-23.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3356.20-23.x86_64.rpm) | 
| Pacote Debian do Ubuntu 18.04 | 14.0.3356.20-23 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3356.20-23_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3356.20-23_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3356.20-23_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu21-july-2020"></a><a id="CU21"></a> CU21 (julho de 2020)

Esta é a versão da Atualização Cumulativa 21 (CU21) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] dela é 14.0.3335.7. Para obter informações sobre as correções e aprimoramentos nesta versão, confira <https://support.microsoft.com/help/4557397>.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

> [!NOTE]
> O **Ubuntu 18.04** e o **RHEL 8** agora são compatíveis com o SQL Server 2017 a partir da CU20.
>
> Os links de instalação do pacote offline do Ubuntu apontam para os pacotes do Ubuntu 18.04, exceto para o pacote SSIS (que não está disponível para o Ubuntu 18.04). Se você estiver procurando pacotes do Ubuntu 16.04, confira o caminho para baixar <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/>.
>
> Os links de instalação do pacote offline do Red Hat apontam para os pacotes do RHEL 8, exceto para o pacote SSIS (que não está disponível para o RHEL 8). Se você estiver procurando pacotes do RHEL 7, confira o caminho para baixar <https://packages.microsoft.com/rhel/7/mssql-server-2017/>.

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3335.7-17 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-14.0.3335.7-17.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-ha-14.0.3335.7-17.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-fts-14.0.3335.7-17.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3335.7-17 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3335.7-17.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3335.7-17.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3335.7-17.x86_64.rpm) | 
| Pacote Debian do Ubuntu 18.04 | 14.0.3335.7-17 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3335.7-17_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3335.7-17_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3335.7-17_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu20-april-2020"></a><a id="CU20"></a> CU20 (abril de 2020)

Esta é a versão da Atualização Cumulativa 20 (CU20) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] dela é 14.0.3294.2. Para obter informações sobre as correções e aprimoramentos nesta versão, confira <https://support.microsoft.com/help/4541283>.

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

> [!NOTE]
> O **Ubuntu 18.04** e o **RHEL 8** agora são compatíveis com o SQL Server 2017 a partir da CU20.
>
> Os links de instalação do pacote offline do Ubuntu apontam para os pacotes do Ubuntu 18.04, exceto para o pacote SSIS (que não está disponível para o Ubuntu 18.04). Se você estiver procurando pacotes do Ubuntu 16.04, confira o caminho para baixar <https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/>.
>
> Os links de instalação do pacote offline do Red Hat apontam para os pacotes do RHEL 8, exceto para o pacote SSIS (que não está disponível para o RHEL 8). Se você estiver procurando pacotes do RHEL 7, confira o caminho para baixar <https://packages.microsoft.com/rhel/7/mssql-server-2017/>.

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3294.2-27 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-14.0.3294.2-27.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-ha-14.0.3294.2-27.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/8/mssql-server-2017/mssql-server-fts-14.0.3294.2-27.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3294.2-27 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3294.2-27.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3294.2-27.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3294.2-27.x86_64.rpm) | 
| Pacote Debian do Ubuntu 18.04 | 14.0.3294.2-27 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3294.2-27_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3294.2-27_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/18.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3294.2-27_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu19-february-2020"></a><a id="CU19"></a> CU19 (fevereiro de 2020)

Esta é a versão CU19 (Atualização Cumulativa 19) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] para esta liberação é 14.0.3281.6. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4535007](https://support.microsoft.com/help/4535007).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3281.6-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3281.6-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3281.6-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3281.6-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3281.6-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3281.6-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3281.6-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3281.6-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3281.6-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3281.6-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3281.6-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3281.6-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu18-december-2019"></a><a id="CU18"></a> CU18 (dezembro de 2019)

Esta é a versão CU18 (Atualização Cumulativa 18) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] dela é 14.0.3257.3. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4527377](https://support.microsoft.com/help/4527377).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3257.3-13 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3257.3-13.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3257.3-13.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3257.3-13.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3257.3-13 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3257.3-13.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3257.3-13.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3257.3-13.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3257.3-13 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3257.3-13_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3257.3-13_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3257.3-13_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

### <a name="added-support"></a>Suporte adicionado

- A CDA (Captura de Dados de Alterações) tem suporte no SQL Server 2017 no Linux da CU18 em diante.
- A Replicação Transacional tem suporte no SQL Server 2017 no Linux da CU18 em diante.

### <a name="remarks"></a>Comentários

Os contêineres do SQL Server 2017 agora têm um novo padrão de marcação, conforme descrito abaixo com exemplos.

- `mcr.microsoft.com/mssql/server:<SQL Server Version>-<update>-<Linux Distribution>-<Linux Distribution Version>`

  Isso efetuará o pull da imagem de contêiner com a combinação descrita na tag.

- `mcr.microsoft.com/mssql/server:<SQL Server Version>-latest`

    Isso efetuará o pull da versão mais recente do SQL Server na versão mais recente do Ubuntu compatível.

**Exemplos:**

`mcr.microsoft.com/mssql/server:2017-CU18-ubuntu-16.04`

Isso efetuará pull SQL Server 2017 CU18 com base no contêiner do Ubuntu 16.04.

`mcr.microsoft.com/mssql/server:2017-latest`

Isso efetuará o pull da versão mais recente do SQL Server 2017 (CU18 no momento em que este artigo foi escrito) com base no contêiner do Ubuntu 16.04.

> [!NOTE]
> Não publicaremos mais contêineres com outros padrões de marcação para contêineres do SQL Server 2017 no futuro.


## <a name="cu17-october-2019"></a><a id="CU17"></a> CU17 (outubro de 2019)

Esta é a versão CU17 (Atualização Cumulativa 17) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] dela é 14.0.3238.1. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4515579](https://support.microsoft.com/help/4515579).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3238.1-19 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3238.1-19.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3238.1-19.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3238.1-19.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3238.1-19 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3238.1-19.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3238.1-19.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3238.1-19.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3238.1-19 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3238.1-19_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3238.1-19_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3238.1-19_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu16-august-2019"></a><a id="CU16"></a> CU16 (agosto de 2019)

Esta é a versão CU16 (Atualização Cumulativa 16) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] dela é 14.0.3223.3. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4508218](https://support.microsoft.com/help/4508218).

### <a name="whats-new"></a>What's New

|Novo recurso ou atualização | Detalhes |
|:---|:---|
| Suporte do MSDTC | Suporte para MSDTC (Coordenador de Transações Distribuídas da Microsoft) para SQL Server 2017. Para saber mais, confira [Como configurar o MSDTC (Coordenador de Transações Distribuídas da Microsoft) no Linux](sql-server-linux-configure-msdtc.md). |

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3223.3-15 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3223.3-15.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3223.3-15.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3223.3-15.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3223.3-15 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3223.3-15.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3223.3-15.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3223.3-15.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3223.3-15 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3223.3-15_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3223.3-15_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3223.3-15_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu15-may-2019"></a><a id="CU15"></a> CU15 (maio de 2019)

Esta é a versão da Atualização Cumulativa 15 (CU15) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3162.1. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4498951](https://support.microsoft.com/help/4498951).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3162.1-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3162.1-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3162.1-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3162.1-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3162.1-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3162.1-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3162.1-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3162.1-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3162.1-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu14-mar-2019"></a><a id="CU14"></a> CU14 (março de 2019)

Esta é a versão da Atualização Cumulativa 14 (CU14) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3076.1. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4484710](https://support.microsoft.com/help/4484710).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3076.1-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3076.1-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3076.1-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3076.1-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3076.1-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3076.1-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3076.1-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3076.1-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3076.1-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu13-dec-2018"></a><a id="CU13"></a> CU13 (dezembro de 2018)

Esta é a versão da Atualização Cumulativa 13 (CU13) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3048.4. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4466404](https://support.microsoft.com/help/4466404).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3048.4-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3048.4-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3048.4-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3048.4-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3048.4-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3048.4-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3048.4-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3048.4-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3048.4-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu12-oct-2018"></a><a id="CU12"></a> CU12 (outubro de 2018)

Esta é a versão da Atualização Cumulativa 12 (CU12) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3045.24. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4464082](https://support.microsoft.com/help/4464082).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3045.24-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3045.24-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3045.24-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3045.24-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3045.24-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3045.24-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3045.24-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3045.24-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3045.24-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu11-sept-2018"></a><a id="CU11"></a> CU11 (setembro de 2018)

Esta é a versão da Atualização Cumulativa 11 (CU11) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3038.14. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4462262](https://support.microsoft.com/help/4462262).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3038.14-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3038.14-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3038.14-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3038.14-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3038.14-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3038.14-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3038.14-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3038.14-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3038.14-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu10-aug-2018"></a><a id="CU10"></a> CU10 (agosto de 2018)

Esta é a versão da Atualização Cumulativa 10 (CU10) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3037.1. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4342123](https://support.microsoft.com/help/4342123).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3037.1-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3037.1-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3037.1-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3037.1-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3037.1-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3037.1-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3037.1-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3037.1-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3037.1-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu9-gdr2-aug-2018"></a><a id="CU9-GDR2"></a> CU9-GDR2 (agosto de 2018)

Esta é uma atualização de segurança que também inclui a CU lançada anteriormente (CU9) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3035.2. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4293805](https://support.microsoft.com/help/4293805).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3035.2-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm)| 
| Pacote RPM do SLES | 14.0.3035.2-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3035.2-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3035.2-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3035.2-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3035.2-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3035.2-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3035.2-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3035.2-1_amd64.deb)<br/> |

## <a name="gdr2-aug-2018"></a><a id="GDR2"></a> GDR2 (agosto de 2018)

Esta é uma atualização de segurança que inclui apenas as correções de segurança do GDR2 (e do GDR1) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)].  A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.2002.14. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4293803](https://support.microsoft.com/help/4293803).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.2002.14-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.2002.14-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2002.14-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2002.14-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2002.14-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.2002.14-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2002.14-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2002.14-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2002.14-1_amd64.deb) |

## <a name="cu9-jul-2018"></a><a id="CU9"></a> CU9 (julho de 2018)

Esta é a versão da Atualização Cumulativa 9 (CU9) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3030.27. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4341265](https://support.microsoft.com/help/4341265).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3030.27-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3030.27-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3030.27-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3030.27-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3030.27-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3030.27-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3030.27-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3030.27-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3030.27-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu8-jun-2018"></a><a id="CU8"></a> CU8 (junho de 2018)

Esta é a versão da Atualização Cumulativa 8 (CU8) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3029.16. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4338363](https://support.microsoft.com/help/4338363).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3029.16-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3029.16-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3029.16-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3029.16-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3029.16-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3029.16-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3029.16-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3029.16-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3029.16-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu7-may-2018"></a><a id="CU7"></a> CU7 (maio de 2018)

Esta é a versão da Atualização Cumulativa 7 (CU7) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3026.27. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4229789](https://support.microsoft.com/help/4229789).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3026.27-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3026.27-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3026.27-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3026.27-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3026.27-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3026.27-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3026.27-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3026.27-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3026.27-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu6-apr-2018"></a><a id="CU6"></a> CU6 (abril de 2018)

Esta é a versão da Atualização Cumulativa 6 (CU6) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3025.34. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4101464](https://support.microsoft.com/help/4101464).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3025.34-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3025.34-3 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3025.34-3.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3025.34-3.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3025.34-3.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3025.34-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3025.34-3_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3025.34-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3025.34-3_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu5-mar-2018"></a><a id="CU5"></a> CU5 (março do 2018)

Esta é a versão da Atualização Cumulativa 5 (CU5) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3023.8. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4092643](https://support.microsoft.com/help/4092643).

### <a name="known-upgrade-issue"></a>Problemas de atualização conhecidos

Quando você atualiza de uma versão anterior para a CU5, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pode falhar ao ser iniciado, retornando o seguinte erro:

```
Error: 4860, Severity: 16, State: 1.
Cannot bulk load. The file "C:\Install\SqlTraceCollect.dtsx" does not exist or you don't have file access rights.
Error: 912, Severity: 21, State: 2.
Script level upgrade for database 'master' failed because upgrade step 'msdb110_upgrade.sql' encountered error 200, state
```

Para resolver esse erro, habilite o SQL Server Agent e reinicie o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com os seguintes comandos:

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
sudo systemctl start mssql-server
```

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3023.8-5 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3023.8-5 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3023.8-5.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3023.8-5.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3023.8-5.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3023.8-5 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3023.8-5_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3023.8-5_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3023.8-5_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu4-feb-2018"></a><a id="CU4"></a> CU4 (fevereiro de 2018)

Esta é a versão da Atualização Cumulativa 4 (CU4) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3022.28. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4056498](https://support.microsoft.com/help/4056498).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

> [!NOTE]
> Desde a CU4, o SQL Server Agent não é mais instalado como um pacote separado. Ele é instalado com o pacote do mecanismo e precisa ser habilitado para ser usado.

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3022.28-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3022.28-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3022.28-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3022.28-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3022.28-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3022.28-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3022.28-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3022.28-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3022.28-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="gdr1-jan-2018"></a><a id="GDR1"></a> GDR1 (janeiro de 2018)

Esta é uma atualização de segurança que inclui apenas as correções de segurança do GDR1 para o [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.2000.63. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4057122](https://support.microsoft.com/help/4057122).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.2000.63-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.2000.63-3 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-14.0.2000.63-3.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-ha-14.0.2000.63-3.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017-gdr/mssql-server-fts-14.0.2000.63-3.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.2000.63-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server/mssql-server_14.0.2000.63-3_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.2000.63-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017-gdr/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.2000.63-3_amd64.deb) |

## <a name="cu3-jan-2018"></a><a id="CU3"></a> CU3 (janeiro de 2018)

Esta é a versão da Atualização Cumulativa 3 (CU3) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3015.40. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4052987](https://support.microsoft.com/help/4052987).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3015.40-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3015.40-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3015.40-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3015.40-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3015.40-1.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3015.40-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3015.40-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3015.40-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3015.40-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu2-nov-2017"></a><a id="CU2"></a> CU2 (novembro de 2017)

Esta é a versão da Atualização Cumulativa 2 (CU2) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3008.27. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/4052574](https://support.microsoft.com/help/4052574).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3008.27-1 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3008.27-1 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3008.27-1.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3008.27-1.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3008.27-1.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3008.27-1.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3008.27-1 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3008.27-1_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3008.27-1_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="cu1-oct-2017"></a><a id="CU1"></a> CU1 (outubro de 2017)

Esta é a versão da Atualização Cumulativa 1 (CU1) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.3006.16. Para obter informações sobre as correções e melhorias nesta versão, confira [https://support.microsoft.com/help/KB4053439](https://support.microsoft.com/help/4038634).

### <a name="package-details"></a>Detalhes do pacote

Para instalações de pacotes manuais ou offline, você pode baixar os pacotes RPM e Debian com as informações na tabela a seguir:

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.3006.16-3 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.3006.16-3 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.3006.16-3.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.3006.16-3.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.3006.16-3.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.3006.16-3.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.3006.16-3 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.3006.16-3_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.3006.16-3_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="ga-oct-2017"></a><a id="GA"></a> GA (outubro de 2017)

Esta é a versão de GA (disponibilidade geral) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. A versão [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] desta versão é 14.0.1000.169.

### <a name="package-details"></a>Detalhes do pacote

Os detalhes do pacote e os locais de download dos pacotes RPM e Debian estão listados na tabela a seguir. Não será necessário baixar esses pacotes diretamente se você seguir as etapas nos seguintes guias de instalação:

- [Instalar pacote do SQL Server](sql-server-linux-setup.md)
- [Instalar pacote de Pesquisa de texto completo](sql-server-linux-setup-full-text-search.md)
- [Instalar pacote do SQL Server Agent](sql-server-linux-setup-sql-agent.md)
- [Instalar o SQL Server Integration Services](sql-server-linux-setup-ssis.md)

| Pacote | Versão do pacote | Downloads |
|-----|-----|-----|
| Pacote RPM do Red Hat | 14.0.1000.169-2 | [Pacote RPM do mecanismo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm)</br>[Pacote SSIS](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-is-14.0.1000.169-1.x86_64.rpm) | 
| Pacote RPM do SLES | 14.0.1000.169-2 | [Pacote RPM do mecanismo mssql-server](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-14.0.1000.169-2.x86_64.rpm)</br>[Pacote RPM de Alta Disponibilidade](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-ha-14.0.1000.169-2.x86_64.rpm)</br>[Pacote RPM de pesquisa de texto completo](https://packages.microsoft.com/sles/12/mssql-server-2017/mssql-server-fts-14.0.1000.169-2.x86_64.rpm)</br>[Pacote de RPM SQL Server Agent](https://packages.microsoft.com/rhel/7/mssql-server-2017/mssql-server-agent-14.0.1000.169-2.x86_64.rpm) | 
| Pacote Debian do Ubuntu 16.04 | 14.0.1000.169-2 | [Pacote Debian do mecanismo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server/mssql-server_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian de alta disponibilidade](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-ha/mssql-server-ha_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian de pesquisa de texto completo](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-fts/mssql-server-fts_14.0.1000.169-2_amd64.deb)</br>[Pacote Debian do SQL Server Agent](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-agent/mssql-server-agent_14.0.1000.169-2_amd64.deb)<br/>[Pacote SSIS](https://packages.microsoft.com/ubuntu/16.04/mssql-server-2017/pool/main/m/mssql-server-is/mssql-server-is_14.0.1000.169-1_amd64.deb) |

## <a name="known-issues"></a>Problemas conhecidos

As seções a seguir descrevem problemas conhecidos com a versão de GA (Disponibilidade geral) do [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] em Linux.

#### <a name="general"></a>Geral

- O comprimento do nome do host em que [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é instalado precisa ter 15 caracteres ou menos. 

    - **Resolução:** altere o nome em /etc/hostname para algo com 15 caracteres de comprimento ou menos.

- Definir manualmente a hora do sistema de maneira a voltar no tempo fará com que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pare de atualizar a hora do sistema interno dentro do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

    - **Resolução:** Reinicie o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].

- Há suporte apenas para instalações de instância única.

    - **Resolução:** Se quiser ter mais de uma instância em um determinado host, considere usar VMs ou contêineres do Docker. 

- [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] O Configuration Manager não pode se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Linux.

- O idioma padrão do logon de **sa** é inglês.

    - **Resolução:** Altere o idioma do logon do **sa** usando a instrução **ALTER LOGIN**.

#### <a name="databases"></a>Bancos de dados

- O banco de dados mestre não pode ser movido com o utilitário mssql-conf. Outros bancos de dados do sistema podem ser movidos usando mssql-conf.

- Ao restaurar um banco de dados do qual foi feito backup no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Windows, você deve usar a cláusula **WITH MOVE** na instrução Transact-SQL.

- Certos algoritmos (pacotes de criptografia) para o protocolo TLS não funcionam corretamente com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux. Isso causa falhas de conexão ao tentar se conectar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], bem como problemas de estabelecimento de conexões entre réplicas em grupos de alta disponibilidade.

   - **Resolução:** modifique o script de configuração **mssql.conf** para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux para desabilitar pacotes de criptografia problemáticos, fazendo o seguinte:

      1. Adicione o seguinte a /var/opt/mssql/mssql.conf.

         ```
         [network]
         tlsciphers= AES256-GCM-SHA384:AES128-GCM-SHA256:AES256-SHA256:AES128-SHA256:AES256-SHA:AES128-SHA:!ECDHE-RSA-AES128-GCM-SHA256:!ECDHE-RSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES256-GCM-SHA384:!ECDHE-ECDSA-AES128-GCM-SHA256:!ECDHE-ECDSA-AES256-SHA384:!ECDHE-ECDSA-AES128-SHA256:!ECDHE-ECDSA-AES256-SHA:!ECDHE-ECDSA-AES128-SHA:!ECDHE-RSA-AES256-SHA384:!ECDHE-RSA-AES128-SHA256:!ECDHE-RSA-AES256-SHA:!ECDHE-RSA-AES128-SHA:!DHE-RSA-AES256-GCM-SHA384:!DHE-RSA-AES128-GCM-SHA256:!DHE-RSA-AES256-SHA:!DHE-RSA-AES128-SHA:!DHE-DSS-AES256-SHA256:!DHE-DSS-AES128-SHA256:!DHE-DSS-AES256-SHA:!DHE-DSS-AES128-SHA:!DHE-DSS-DES-CBC3-SHA:!NULL-SHA256:!NULL-SHA
         ```

         > [!NOTE]
         > No código anterior, `!` nega a expressão. Isso informa ao OpenSSL para não usar o conjunto de codificação a seguir.  

      1. Reinicie o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com o seguinte comando.

         ```bash
         sudo systemctl restart mssql-server
         ```

- Bancos de dados do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] no Windows que usam OLTP in-memory não podem ser restaurados no [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] no Linux. Para restaurar um banco de dados do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] que usa OLTP in-memory, primeiro atualize os bancos de dados para [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] ou [!INCLUDE[ssSQL17](../includes/sssql17-md.md)] no Windows antes de movê-los para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em Linux por meio de backup/restauração ou de desanexar/anexar.

- A permissão de usuário **ADMINISTRAR OPERAÇÕES EM MASSA** não tem suporte no Linux no momento.

#### <a name="networking"></a>Rede

Recursos que envolvem conexões TCP de saída do processo sqlservr, como servidores vinculados ou Grupos de Disponibilidade, poderão não funcionar se ambas as condições a seguir forem atendidas:

1. O servidor de destino é especificado como um nome de host e não como um endereço IP.

1. A instância de origem tem IPv6 desabilitado no kernel. Para verificar se o sistema tem o IPv6 habilitado no kernel, todos os testes a seguir precisam ser aprovados:

   - `cat /proc/cmdline` imprimirá o cmdline de inicialização do kernel atual. A saída não deve conter `ipv6.disable=1`.
   - O diretório /proc/sys/net/ipv6/ deve existir.
   - Um programa em C que chama `socket(AF_INET6, SOCK_STREAM, IPPROTO_IP)` deve ter êxito – syscall deve retornar um fd != -1 e não falhar com EAFNOSUPPORT.

O erro exato depende do recurso. Para servidores vinculados, isso se manifesta como um erro de tempo limite de logon. Para grupos de disponibilidade, o DDL do `ALTER AVAILABILITY GROUP JOIN` no secundário falhará após 5 minutos com um erro de tempo limite de configuração de download.

Para contornar esse problema, adote uma das seguintes medidas:

1. Use IPs em vez de nomes do host para especificar o destino da conexão TCP.

1. Habilite o IPv6 no kernel removendo `ipv6.disable=1` da inicialização de cmdline. A maneira de fazer isso depende da distribuição do Linux e do carregador de inicialização, como o grub. Se você deseja que o IPv6 seja desabilitado, ainda pode desativá-lo definindo `net.ipv6.conf.all.disable_ipv6 = 1` na configuração `sysctl` (por exemplo, `/etc/sysctl.conf`). Isso ainda impedirá que o adaptador de rede do sistema receba um endereço IPv6, mas permitirá que os recursos do sqlservr funcionem.

#### <a name="network-file-system-nfs"></a>NFS (sistema de arquivos de rede)
Se você usar compartilhamentos remotos **NFS (Network File System)** em produção, observe os seguintes requisitos de suporte:

- Use o NFS versão **4.2 ou superior**. As versões mais antigas do NFS não dão suporte aos recursos necessários, como fallocate e criação de arquivos esparsos, comuns aos sistemas de arquivos modernos.
- Localize somente os diretórios **/var/opt/mssql** na montagem NFS. Não há suporte para outros arquivos, como os binários do sistema [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].
- Verifique se os clientes NFS usam a opção 'nolock' ao montar o compartilhamento remoto.

#### <a name="localization"></a>Localização

- Se a sua localidade não for inglês (en_us) durante a instalação, você precisará usar a codificação UTF-8 em sua sessão/terminal de Bash. Se usar a codificação ASCII, você poderá ver um erro semelhante ao seguinte:

   ```
   UnicodeEncodeError: 'ascii' codec can't encode character u'\xf1' in position 8: ordinal not in range(128)
   ```

   Se não for possível usar a codificação UTF-8, você deverá executar a instalação usando a variável de ambiente MSSQL_LCID para especificar sua escolha de idioma.

   ```bash
   sudo MSSQL_LCID=<LcidValue> /opt/mssql/bin/mssql-conf setup
   ```

- Ao executar a instalação de mssql-conf e executar uma instalação de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com idioma diferente do inglês, caracteres estendidos incorretos são exibidos após o texto localizado, "Configurando o SQL Server...". Ou, para instalações não baseadas em latim, a frase pode estar completamente ausente. A frase ausente deve exibir a seguinte cadeia de caracteres localizada: "O PID de licenciamento foi processado com êxito. A nova edição é [\<Name\> Edition]". Essa cadeia de caracteres é fornecida apenas para fins informativos e a próxima Atualização Cumulativa do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] resolverá isso para todos os idiomas. Isso não afetará o êxito da instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de forma alguma. 

#### <a name="full-text-search"></a>Pesquisa de Texto Completo

- Nem todos os filtros estão disponíveis nesta versão, incluindo filtros para documentos do Office. Para obter uma lista de filtros com suporte, confira [Instalar a pesquisa de texto completo do SQL Server no Linux](sql-server-linux-setup-full-text-search.md#filters).

#### <a name="sql-server-integration-services-ssis"></a><a id="ssis"></a> SQL Server Integration Services (SSIS)

- O pacote **mssql-server-is** não tem suporte no SUSE nesta versão. Atualmente, ele tem suporte no Ubuntu e no RHEL (Red Hat Enterprise Linux).

- Com o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] na Atualização CTP 2.1 do Linux e posterior, os pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] podem usar conexões ODBC no Linux. Essa funcionalidade foi testada com o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e os drivers ODBC do MySQL, mas também espera-se que ela funcione com qualquer driver ODBC Unicode que observa a especificação ODBC. Em tempo de design, é possível fornecer um DSN ou uma cadeia de conexão para conectar-se aos dados ODBC; também é possível usar a autenticação do Windows. Para saber mais, confira a [postagem no blog que anunciou o suporte do ODBC para Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

- Não há suporte para os seguintes recursos nesta versão ao executar pacotes SSIS no Linux:
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Banco de dados de catálogo
  - Execução de pacotes agendada pelo SQL Agent
  - Autenticação do Windows
  - Componentes de terceiros
  - Change Data Capture (CDC)
  - [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] Scale Out
  - Feature Pack do Azure para SSIS
  - Suporte para Hadoop e HDFS
  - Microsoft Connector for SAP BW

Para obter uma lista de componentes internos do SSIS que não têm suporte no momento ou que têm suporte com limitações, confira [Limitações e problemas conhecidos do SSIS no Linux](sql-server-linux-ssis-known-issues.md#components).

Para saber mais sobre o SSIS no Linux, confira os seguintes artigos:
-   [Postagem no blog anunciando o suporte do SSIS para Linux](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/).
-   [Instalar o SSIS (SQL Server Integration Services) no Linux](sql-server-linux-setup-ssis.md)
-   [Extrair, transformar e carregar dados no Linux com o SSIS](sql-server-linux-migrate-ssis.md)

#### <a name="sql-server-management-studio-ssms"></a><a id="ssms"></a> SSMS (SQL Server Management Studio)

As seguintes limitações se aplicam ao [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] no Windows conectado ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no Linux.

- Não há suporte para planos de manutenção.

- Não há suporte para a extensão MDW (Data Warehouse de Gerenciamento) e o coletor de dados no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. 

- Componentes da interface do usuário do [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] que têm as opções de Autenticação do Windows ou log de eventos do Windows não funcionam com o Linux. Você ainda pode usar esses recursos com outras opções, como logons do SQL. 

- O número de arquivos de log a serem retidos não pode ser modificado.

## <a name="next-steps"></a>Próximas etapas

Para começar, confira os seguintes guias de início rápido:

- [Instalação no Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalação no SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar no Ubuntu](quickstart-install-connect-ubuntu.md)
- [Executar no Docker](quickstart-install-connect-docker.md)
- [Provisionar uma VM SQL no Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)
- [Executar e conectar – Nuvem](quickstart-install-connect-clouds.md)

Para obter respostas a perguntas frequentes, confira as [Perguntas frequentes sobre o SQL Server em Linux](sql-server-linux-faq.md).
