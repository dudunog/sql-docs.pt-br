---
title: Registrar computador com o Serviço Guardião de Host
description: Registre o computador SQL Server com o Serviço Guardião de Host para Always Encrypted com o enclaves seguros.
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5864ec2b5bda5febc27bbb15606452befe7e293f
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534775"
---
# <a name="register-computer-with-host-guardian-service"></a>Registrar computador com o Serviço Guardião de Host

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Este artigo descreve como registrar computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para atestar com o HGS (Serviço Guardião de Host).

> [!NOTE]
> O processo de registro de um [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] no HGS exige um esforço conjunto do administrador do HGS e do administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]. Confira [Funções e responsabilidades ao configurar o atestado com o HGS](always-encrypted-enclaves-host-guardian-service-plan.md#roles-and-responsibilities-when-configuring-attestation-with-hgs).

Antes de começar, verifique se você implantou, pelo menos, um computador do HGS e configurou o serviço de atestado do HGS.
Confira [Implantar o Serviço Guardião de Host para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]](./always-encrypted-enclaves-host-guardian-service-deploy.md) para obter mais informações.

## <a name="step-1-install-the-attestation-client-components"></a>Etapa 1: Instalar os componentes do cliente de atestado

> [!NOTE]
> Essa etapa deve ser executada pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

Para permitir que um cliente SQL verifique se ele está se comunicando com um computador confiável [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], o computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] deve atestar com êxito com o Serviço Guardião de Host.
O processo de atestado é gerenciado por um componente opcional do Windows chamado de Cliente HGS.
As etapas a seguir ajudarão você a instalar esse componente e iniciar o atestado.

1. Verifique se o computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] cumpre os [pré-requisitos descritos no documento de planejamento do HGS](./always-encrypted-enclaves-host-guardian-service-plan.md#prerequisites).

2. Execute o seguinte comando em um console do PowerShell com privilégios elevados para instalar o recurso de Suporte do Hyper-V do Guardião de Host, que contém o cliente HGS e os componentes de atestado.

    ```powershell
    Enable-WindowsOptionalFeature -Online -FeatureName HostGuardian -All
    ```

3. Reinicie para concluir a instalação.

## <a name="step-2-verify-virtualization-based-security-is-running"></a>Etapa 2: Verificar se a segurança baseada em virtualização está em execução

> [!NOTE]
> Essa etapa deve ser executada pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

Quando você instala o recurso de Suporte do Hyper-V do Guardião de Host, a VBS (segurança baseada em virtualização) é configurada e habilitada automaticamente.
Os enclaves para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted são protegidos e executados dentro do ambiente da VBS.
A VBS poderá não iniciar se o computador não tiver um dispositivo IOMMU instalado e habilitado.
Para verificar se a VBS está em execução, abra a ferramenta Informações do Sistema executando `msinfo32.exe` e localize os itens de `Virtualization-based security` na parte inferior do Resumo do Sistema.

![Captura de tela de informações do sistema mostrando o status e a configuração da segurança baseada em virtualização](./media/always-encrypted-enclaves/msinfo32-vbs-status.png)

O primeiro item a ser verificado é `Virtualization-based security`, que pode ter os três valores seguintes:

- `Running` significa que a VBS está configurada corretamente e foi inicializada com êxito. Se o computador mostrar esse status, você poderá pular para a Etapa 3.
- `Enabled but not running` significa que a VBS está configurada para ser executada, mas o hardware não tem os requisitos mínimos de segurança para executá-la. Talvez seja necessário alterar a configuração do hardware no BIOS ou no UEFI para habilitar recursos opcionais do processador como uma IOMMU ou, se o hardware realmente não oferecer suporte aos recursos necessários, talvez seja necessário reduzir os requisitos de segurança da VBS. Continue lendo esta seção para saber mais.
- `Not enabled` significa que a VBS não está configurada para execução. O recurso de Suporte do Hyper-V do Guardião de Host habilita automaticamente a VBS, portanto, é recomendável repetir a Etapa 1 se você vir esse status.

Se a VBS não estiver em execução no computador, verifique as propriedades do `Virtualization-based security`. Compare os valores no item de `Required Security Properties` com os valores no item de `Available Security Properties`.
As propriedades obrigatórias devem ser iguais a um subconjunto das propriedades de segurança disponíveis para que a VBS seja executada.

No contexto de atestado de enclaves do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], as propriedades de segurança têm a seguinte importância:

- `Base virtualization support` é sempre obrigatório, pois representa os recursos mínimos de hardware necessários para executar um hipervisor.
- `Secure Boot` é recomendado, mas não é obrigatório para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted. A inicialização segura protege contra rootkits exigindo a execução imediata de um carregador de inicialização com assinatura da Microsoft após a conclusão do UEFI. Se você estiver usando o atestado TPM (Trusted Platform Module), a habilitação de inicialização segura será medida e imposta independentemente de a VBS estar configurada para exigir inicialização segura.
- `DMA Protection` é recomendado, mas não é obrigatório para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] Always Encrypted. A proteção de DMA usa uma IOMMU para proteger o enclave e a memória da VBS contra ataques de acesso direto à memória. Em um ambiente de produção, você sempre deve usar computadores com proteção DMA. Em um ambiente de desenvolvimento/teste, não há problema em remover o requisito de proteção de DMA. Se a instância de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] for virtualizada, você provavelmente não terá a proteção de DMA disponível e precisará remover o requisito de execução da VBS. Examine o [modelo de confiança](./always-encrypted-enclaves-host-guardian-service-plan.md#trust-model) para obter informações sobre as garantias de segurança reduzidas durante a execução em uma VM.

Antes de reduzir os recursos de segurança obrigatórios da VBS, verifique com o seu OEM ou provedor de serviços de nuvem para confirmar se há uma forma de habilitar os requisitos de plataforma ausentes na UEFI ou no BIOS (por exemplo, habilitar a Inicialização Segura, a Intel VT-d ou a AMD IOV).

Para alterar os recursos de segurança de plataforma necessários para VBS, execute o seguinte comando em um console do PowerShell com privilégios elevados:

```powershell
# Value 0 = No security features required (use this for Azure VMs)
# Value 1 = Only Secure Boot is required
# Value 2 = Only DMA protection is required (default configuration)
# Value 3 = Both Secure Boot and DMA protection are required
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\DeviceGuard -Name RequirePlatformSecurityFeatures -Value 0
```

Depois de alterar o Registro, reinicie o computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e verifique se a VBS está em execução novamente.

Se o computador for gerenciado por sua empresa, a Política de Grupo ou o Gerenciador de Ponto de Extremidade da Microsoft poderá substituir as alterações feitas nessas chaves de Registro após a reinicialização.
Entre em contato com o suporte técnico de TI para saber se ele implanta políticas que gerenciam sua configuração da VBS.

## <a name="step-3-configure-the-attestation-url"></a>Etapa 3: Configurar a URL de atestado

> [!NOTE]
> Essa etapa deve ser executada pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

Em seguida, você vai configurar o computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] com a URL do serviço de atestado do HGS, obtida com o administrador do HGS.

Em um console do PowerShell com privilégios elevados, atualize e execute o comando a seguir para configurar a URL de atestado.

- Substitua `hgs.bastion.local` pelo nome do cluster do HGS
- Você pode executar `Get-HgsServer` em qualquer computador HGS para obter o nome do cluster
- A URL de atestado sempre deve terminar com `/Attestation`
- O SQL Server não utiliza os principais recursos de proteção do HGS, portanto, informe qualquer URL fictícia como `http://localhost` para `-KeyProtectionServerUrl`

```powershell
Set-HgsClientConfiguration -AttestationServerUrl "https://hgs.bastion.local/Attestation" -KeyProtectionServerUrl "http://localhost"
```

A menos que você tenha registrado este computador com o HGS antes, o comando relatará uma falha de atestado. Esse resultado é normal.

O campo `AttestationMode` na saída do cmdlet indica o modo de atestado que o HGS usa.

Vá para a [Etapa 4A](#step-4a-register-a-computer-in-tpm-mode) para registrar o computador no modo TPM ou para a [Etapa 4B](#step-4b-register-a-computer-in-host-key-mode) para registrar o computador no modo de chave do host.

## <a name="step-4a-register-a-computer-in-tpm-mode"></a>Etapa 4A: Registrar um computador no modo TPM

> [!NOTE]
> Essa etapa é executada em conjunto pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e pelo administrador do HGS. Confira as observações abaixo para obter detalhes.

### <a name="prepare"></a>Preparar

> [!NOTE]
> Essa ação deve ser executada pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

Nesta etapa, você coleta informações sobre o estado do TPM do computador e o registra com o HGS.

Se o serviço de atestado HGS estiver configurado para usar o modo de chave de host, pule para a [Etapa 4B](#step-4b-register-a-computer-in-host-key-mode).

Antes de começar a coletar as medições do TPM, verifique se você está trabalhando em uma configuração válida do computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].
O computador deve ter todo o hardware necessário instalado e as atualizações de firmware e software mais recentes aplicadas.
O HGS mede os computadores com relação a essa linha de base quando eles atestam, portanto, é importante estar no estado desejado e mais seguro possível ao coletar as medições do TPM.

Há três arquivos de dados coletados para atestado de TPM, alguns dos quais poderão ser reutilizados se você tiver computadores configurados de forma idêntica.

| Artefato de atestado | O que ele mede | Exclusividade |
| -------------------- | ---------------- | ---------- |
| Identificador de plataforma  | A chave de endosso pública no TPM do computador e o certificado de chave de endosso do fabricante do TPM. | Uma para cada computador |
| Linha de base do TPM | Os PCRs (registros de controle de plataforma) no TPM que medem o firmware e a configuração do sistema operacional carregados durante o processo de inicialização. Os exemplos incluem o estado de inicialização segura e se os despejos de memória são criptografados. | Configuração de uma linha de base por computador único (hardware e software idênticos podem usar a mesma linha de base) |
| Política de integridade de código | A política de [Controle de Aplicativo do Windows Defender](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control) em que você confia para proteger os computadores | Uma por política de CI exclusiva implantada nos computadores. |

Você pode configurar mais de um artefato de atestado no HGS para dar suporte a uma frota mista de hardware e software.
O HGS requer apenas que um atestado de computador corresponda a uma política de cada categoria de política.
Por exemplo, se você tiver três linhas de base do TPM registradas no HGS, as medições do computador poderão corresponder a qualquer uma dessas linhas de base para cumprir o requisito da política.

### <a name="configure-a-code-integrity-policy"></a>Configurar uma política de integridade de código

> [!NOTE]
> As etapas abaixo devem ser executadas pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

O HGS requer que todos os atestados de computador no modo TPM tenham uma política do WDAC (Controle de Aplicativos do Windows Defender) aplicada.
As políticas de integridade de código WDAC restringem o software que pode ser executado em um computador, verificando cada processo que tenta executar código em uma lista de editores e hashes de arquivo confiáveis.
Para o caso de uso [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], os enclaves são protegidos pela segurança baseada em virtualização e não podem ser modificados no sistema operacional do host, portanto, a restrição da política WDAC não afeta a segurança das consultas criptografadas.
Assim, recomendamos que você implante uma política de modo de auditoria para os computadores do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] a fim de atender ao requisito de atestado sem impor restrições adicionais ao sistema.

Se você já estiver usando uma política de integridade de código WDAC personalizada nos computadores para proteger a configuração do sistema operacional, pule para [Coletar informações de atestado de TPM](#collect-tpm-attestation-information).

1. Há exemplos de políticas previamente disponibilizados em todos os sistemas operacionais Windows Server 2019, Windows 10 versão 1809 e posteriores. A política de `AllowAll` permite que qualquer software seja executado no computador sem restrições. Converta a política em um formato binário compreendido pelo sistema operacional e pelo HGS para usá-la. Em um console do PowerShell com privilégios elevados, execute os seguintes comandos para compilar a política de `AllowAll`:

    ```powershell
    # We are changing the policy to disable enforcement and user mode code protection before compiling
    $temppolicy = "$HOME\Desktop\allowall_edited.xml"
    Copy-Item -Path "$env:SystemRoot\schemas\CodeIntegrity\ExamplePolicies\AllowAll.xml" -Destination $temppolicy
    Set-RuleOption -FilePath $temppolicy -Option 0 -Delete
    Set-RuleOption -FilePath $temppolicy -Option 3

    ConvertFrom-CIPolicy -XmlFilePath $temppolicy -BinaryFilePath "$HOME\Desktop\allowall_cipolicy.bin"
    ```

2. Siga as orientações no [guia de implantação do Controle de Aplicativos do Windows Defender](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide) para implantar o arquivo de `allowall_cipolicy.bin` nos computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] usando a [Política de Grupo](/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-group-policy). Para computadores do grupo de trabalho, siga o mesmo processo usando o Editor de Política de Grupo Local (`gpedit.msc`).

3. Execute `gpupdate /force` nos computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para configurar a nova política de integridade de código e reinicie os computadores para aplicar a política.

### <a name="collect-tpm-attestation-information"></a>Coletar informações de atestado de TPM

> [!NOTE]
> As etapas abaixo devem ser executadas pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

Repita as etapas a seguir para cada computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] que será atestado com o HGS:

1. Com o computador em um estado válido, execute os seguintes comandos no PowerShell para coletar as informações de atestado do TPM:

    ```powershell
    # Collects the TPM EKpub and EKcert
    $name = $env:computername
    $path = "$HOME\Desktop"
    (Get-PlatformIdentifier -Name $name).Save("$path\$name-EK.xml")

    # Collects the TPM baseline (current PCR values)
    Get-HgsAttestationBaselinePolicy -Path "$path\$name.tcglog" -SkipValidation

    # Collects the applied CI policy, if one exists
    Copy-Item -Path "$env:SystemRoot\System32\CodeIntegrity\SIPolicy.p7b" -Destination "$path\$name-CIpolicy.bin"
    ```

2. Compartilhe os três arquivos de atestado com o administrador do HGS. 

### <a name="register-the-sql-server-computer-with-hgs"></a>Registrar o computador do SQL Server no HGS

> [!NOTE]
> As etapas abaixo devem ser executadas pelo administrador do HGS.

Repita as etapas a seguir para cada computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] que será atestado com o HGS:

1. Copie os arquivos de atestado obtidos com o administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para o servidor do HGS. 
2. No servidor HGS, execute os seguintes comandos em um console do PowerShell com privilégios elevados para registrar o computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]:

    ```powershell
    # TIP: REMEMBER TO CHANGE THE FILENAMES
    # Registers the unique TPM with HGS (required for every computer)
    Add-HgsAttestationTpmHost -Path "C:\temp\SQL01-EK.xml"

    # Registers the TPM baseline (required ONCE for each unique hardware and software configuration)
    Add-HgsAttestationTpmPolicy -Name "MyHWSoftwareConfig" -Path "C:\temp\SQL01.tcglog"

    # Registers the CI policy (required ONCE for each unique CI policy)
    Add-HgsAttestationCiPolicy -Name "AllowAll" -Path "C:\temp\SQL01-CIpolicy.bin"
    ```

    > [!TIP]
    > Se você encontrar um erro ao tentar registrar o identificador exclusivo do TPM, verifique se você [importou os certificados raiz e intermediário do TPM](./always-encrypted-enclaves-host-guardian-service-deploy.md#switch-to-tpm-attestation) no computador do HGS que você está usando.

Além do identificador de plataforma, da linha de base do TPM e da política de integridade de código, há políticas internas configuradas e impostas pelo HGS que talvez você precise alterar.
Essas políticas internas são medidas da linha de base do TPM que você coleta do servidor e declaram uma variedade de configurações de segurança que devem ser habilitadas para proteger o computador.
Se você tiver computadores que não tenham uma IOMMU presente para proteger contra ataques DMA (por exemplo, uma VM), você precisará desabilitar a política de IOMMU.

Para desabilitar o requisito de IOMMU, execute o seguinte comando no servidor HGS:

```powershell
Disable-HgsAttestationPolicy Hgs_IommuEnabled
```

> [!NOTE]
> Se você desabilitar a política de IOMMU, IOMMUs não serão exigidas para o atestado de nenhum computador com HGS.
> Não é possível desabilitar a política de IOMMU para apenas um computador.

Você pode examinar a lista de políticas e hosts do TPM registrados com os seguintes comandos do PowerShell:

```powershell
Get-HgsAttestationTpmHost
Get-HgsAttestationTpmPolicy
```

## <a name="step-4b-register-a-computer-in-host-key-mode"></a>Etapa 4B: Registrar um computador no modo de chave do host

> [!NOTE]
> Essa etapa é executada em conjunto pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e pelo administrador do HGS. Confira as observações abaixo para obter detalhes.

Esta etapa explicará o processo para gerar uma chave exclusiva para o host e registrá-la com o HGS.
Se o serviço de atestado HGS estiver configurado para usar o modo TPM, siga as orientações na [Etapa 4A](#step-4a-register-a-computer-in-tpm-mode).

### <a name="generate-a-key-for-a-ssnoversion-md-computer"></a>Gerar uma chave para um computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]

> [!NOTE]
> Essa parte deve ser executada em conjunto pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

O atestado de chave de host funciona gerando um par de chaves assimétricas no computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e fornecendo ao HGS a metade pública dessa chave.

Repita as etapas a seguir para cada computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] que será atestado com o HGS:

1. Para gerar o par de chaves, execute o comando a seguir em um console do Azure PowerShell com privilégios elevados:

    ```powershell
    Set-HgsClientHostKey
    Get-HgsClientHostKey -Path "$HOME\Desktop\$env:computername-key.cer"
    ```

    Se você já tiver criado uma chave de host e quiser gerar um novo par de chaves, use os seguintes comandos:

    ```powershell
    Remove-HgsClientHostKey
    Set-HgsClientHostKey
    Get-HgsClientHostKey -Path "$HOME\Desktop\$env:computername-key.cer"
    ```

2. Compartilhe o arquivo de certificado com o administrador do HGS.

### <a name="register-the-sql-server-computer-with-hgs"></a>Registrar o computador do SQL Server no HGS

> [!NOTE]
> As etapas abaixo devem ser executadas pelo administrador do HGS.

Repita as etapas a seguir para cada computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] que será atestado com o HGS:

1. Copie o arquivo de certificado, obtido com o administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], para um servidor do HGS.
2. Execute os seguintes comandos em um console do PowerShell com privilégios elevados para registrar o computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]:

    ```powershell
    Add-HgsAttestationHostKey -Name "YourComputerName" -Path "C:\temp\yourcomputername.cer"
   ```

## <a name="step-5-confirm-the-host-can-attest-successfully"></a>Etapa 5: Confirmar se o host pode atestar com êxito

> [!NOTE]
> Essa etapa deve ser executada pelo administrador do computador do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].

Depois de registrar o computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] com o HGS ([Etapa 4A](#step-4a-register-a-computer-in-tpm-mode) para o modo TPM, [Etapa 4B](#step-4b-register-a-computer-in-host-key-mode) para o modo de chave do host), você deve confirmar se ele é capaz de atestar com êxito.

Você pode verificar a configuração do cliente de atestado do HGS e executar uma tentativa de atestado a qualquer momento com [Get-HgsClientConfiguration](/powershell/module/hgsclient/get-hgsclientconfiguration?view=win10-ps&preserve-view=true).

A saída do comando terá uma aparência semelhante à seguinte:

```
PS C:\> Get-HgsClientConfiguration


IsHostGuarded                  : True
Mode                           : HostGuardianService
KeyProtectionServerUrl         : http://localhost
AttestationServerUrl           : http://hgs.bastion.local/Attestation
AttestationOperationMode       : HostKey
AttestationStatus              : Passed
AttestationSubstatus           : NoInformation
FallbackKeyProtectionServerUrl :
FallbackAttestationServerUrl   :
IsFallbackInUse                : False
```

Os dois campos mais importantes na saída são `AttestationStatus`, que informa se o computador foi aprovado no atestado e `AttestationSubStatus`, que explica em quais políticas o computador falhou se o computador tiver sido reprovado no atestado.

Os valores mais comuns que podem aparecer em `AttestationStatus` são explicados abaixo:

| `AttestationStatus` | Explicação |
| ----------------- | ----------- |
| Expirado | O host foi aprovado no atestado anteriormente, mas o certificado de integridade que ele foi emitido expirou. Verifique se o host e a hora do HGS estão em sincronia. |
| `InsecureHostConfiguration` | O computador não cumpriu uma ou mais das políticas de atestado configuradas no servidor do HGS. Para obter mais informações, consulte `AttestationSubStatus`. |
| NotConfigured | O computador não está configurado com uma URL de atestado. [Configurar a URL de atestado](#step-3-configure-the-attestation-url) |
| Aprovado | O computador passou pelo atestado e é confiável para executar enclaves [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]. |
| `TransientError` | Falha na tentativa de atestado devido a um erro temporário. Esse erro geralmente significa que houve um problema ao entrar em contato com o HGS pela rede. Verifique a conexão de rede e se o computador pode resolver e rotear para o nome do serviço HGS. |
| `TpmError` | O dispositivo TPM do computador relatou um erro durante a tentativa de atestado. Verifique os logs do TPM para obter mais informações. A limpeza do TPM pode resolver o problema, mas tome cuidado para suspender o BitLocker e outros serviços que dependem do TPM antes de limpar o TPM. |
| `UnauthorizedHost` | A chave do host não é conhecida pelo HGS. Siga as instruções na [Etapa 4B](#step-4b-register-a-computer-in-host-key-mode) para registrar o computador com o HGS. |

Quando o `AttestationStatus` mostrar `InsecureHostConfiguration`, o campo `AttestationSubStatus` será preenchido com um ou mais nomes de política que falharam.
A tabela a seguir explica os valores mais comuns e como corrigir os erros.

| AttestationSubStatus | O que significa e o que fazer |
| -------------------- | ---------------------------- |
| CodeIntegrityPolicy | A política de integridade de código no computador não está registrada com o HGS *ou* o computador não está usando uma política de integridade de código no momento. Confira [Configurar uma política de integridade de código](#configure-a-code-integrity-policy) para obter diretrizes. |
| DumpsEnabled | O computador está configurado para permitir despejos de memória, mas a política Hgs_DumpsEnabled não permite despejos. Desabilite os despejos neste computador ou desabilite a política Hgs_DumpsEnabled para continuar. |
| FullBoot | O computador voltou de um estado de suspensão ou hibernação, resultando em alterações nas medições do TPM. Reinicie o computador para gerar medições de TPM limpas. |
| HibernationEnabled | O computador está configurado para permitir a hibernação com arquivos de hibernação não criptografados. Desabilite a hibernação no computador para resolver esse problema. |
| HypervisorEnforcedCodeIntegrityPolicy | O computador não está configurado para usar uma política de integridade de código. Verifique o Política de Grupo ou a Política de Grupo Local > Configuração do computador > Modelos Administrativos > Sistema > Device Guard > Ativar a Segurança Baseada em Virtualização > Proteção Baseada em Virtualização de Integridade de Código. Esse item de política deve ser "Habilitado sem bloqueio de UEFI". |
| Iommu | Este computador não tem um dispositivo IOMMU habilitado. Se for um computador físico, habilite a IOMMU no menu de configuração UEFI. Se for uma máquina virtual e uma IOMMU não estiver disponível, execute `Disable-HgsAttestationPolicy Hgs_IommuEnabled` no servidor do HGS. |
| SecureBoot | A Inicialização Segura não está habilitada neste computador. Habilite a inicialização segura no menu de configuração UEFI para resolver esse erro. |
| VirtualSecureMode | A segurança baseada em virtualização não está em execução neste computador. Siga as orientações na [Etapa 2: Verificar se a VBS está em execução no computador](#step-2-verify-virtualization-based-security-is-running). |

## <a name="next-steps"></a>Próximas etapas

- [Configurar o enclave seguro no SQL Server](always-encrypted-enclaves-configure-enclave-type.md)