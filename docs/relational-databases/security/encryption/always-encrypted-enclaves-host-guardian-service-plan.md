---
title: Planejar o atestado do Serviço Guardião de Host
description: Planeje o atestado do Serviço Guardião de host para SQL Server Always Encrypted com enclaves seguros.
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: rpsqrd
ms.author: ryanpu
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c4c80a51370de62410367b1225fd85e3ffe7f261
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534795"
---
# <a name="plan-for-host-guardian-service-attestation"></a>Planejar o atestado do Serviço Guardião de Host

[!INCLUDE [sqlserver2019-windows-only](../../../includes/applies-to-version/sqlserver2019-windows-only.md)]

Ao usar o [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md), o aplicativo cliente deve estar se comunicando com um enclave confiável no processo [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]. Para um enclave de VBS (segurança baseada em virtualização), esse requisito inclui verificar se o código dentro do enclave é válido e se o computador que hospeda o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] é confiável. O atestado remoto alcança essa meta introduzindo um terceiro que pode validar a identidade (e, opcionalmente, a configuração) do computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]. Antes que [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] possa usar um enclave para executar uma consulta, ele deve fornecer informações ao serviço de atestado sobre seu ambiente operacional para obter um certificado de integridade. Esse certificado de integridade é enviado para o cliente, que pode verificar de forma independente sua autenticidade com o serviço de atestado. Depois que o cliente confia no certificado de integridade, ele sabe que está se comunicando com um enclave VBS confiável e emitirá a consulta que usará esse enclave.

A função HGS (Serviço Guardião de Host) no Windows Server 2019 fornece recursos de atestado remoto para Always Encrypted com enclaves VBS.
Este artigo orientará você pelas decisões e requisitos de pré-implantação para usar Always Encrypted com enclaves VBS e atestado HGS.

## <a name="architecture-overview"></a>Visão geral da arquitetura

O HGS (Serviço Guardião de Host) é um serviço Web clusterizado que é executado no Windows Server 2019.
Em uma implantação típica, haverá de um a três servidores HGS, pelo menos um computador executando [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e um computador executando um aplicativo cliente ou ferramentas, como o SQL Server Management Studio.
Como o HGS é responsável por determinar quais computadores que executam [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] são confiáveis, ele requer isolamento físico e lógico da instância [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] que está protegendo.
Se os mesmos administradores tiverem acesso ao HGS e a um computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], eles poderão configurar o serviço de atestado para permitir que um computador mal-intencionado execute [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], permitindo que eles comprometam o enclave VBS.

### <a name="hgs-domain"></a>Domínio HGS

A instalação do HGS criará automaticamente um domínio Active Directory para os servidores HGS, os recursos de cluster de failover e as contas de administrador.

O computador que executa o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] não precisa estar em um domínio, mas, se estiver, deverá ser um domínio diferente daquele usado pelo servidor HGS.

### <a name="high-availability"></a>Alta disponibilidade

O recurso HGS instala e configura automaticamente um cluster de failover.
Em um ambiente de produção, é recomendável usar três servidores HGS para alta disponibilidade. Veja a [documentação do cluster de failover](/windows-server/failover-clustering/manage-cluster-quorum) para obter detalhes sobre como o quorum de cluster é determinado e configurações alternativas, incluindo clusters de dois nós com uma testemunha externa.

O armazenamento compartilhado não é necessário entre os nós HGS. Uma cópia do banco de dados de atestado é armazenada em cada servidor HGS e é replicada automaticamente pela rede pelo serviço de cluster.

### <a name="network-connectivity"></a>Conectividade de rede

Tanto o cliente SQL quanto o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] precisa conseguir se comunicar com o HGS por HTTP.
Configure o HGS com um certificado TLS para criptografar todas as comunicações entre o cliente SQL e o HGS, bem como entre o SQL Server e o HGS.
Essa configuração ajuda na proteção contra ataques man-in-the-middle e garante que você esteja se comunicando com o servidor HGS correto.

Os servidores HGS exigem conectividade entre cada nó no cluster para garantir que o banco de dados do serviço de atestado permaneça em sincronia. É uma melhor prática de cluster de failover conectar os nós HGS em uma rede para comunicação de cluster e usar uma rede separada para que outros clientes se comuniquem com o HGS.

### <a name="attestation-modes"></a>Modos de atestado

Quando um computador executando o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] tenta atestar com o HGS, ele primeiro pergunta ao HGS como ele deve atestar.
O HGS é compatível com dois modos de atestado para uso com [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]:

| Modo de atestado | Explicação |
| ---------------- | ------- |
| TPM | O atestado TPM (Trusted Platform Module) fornece a garantia mais forte sobre a identidade e a integridade do atestado do computador com o HGS. Ele requer que os computadores que executam o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] tenham a versão 2.0 do TPM instalada. Cada chip do TPM contém uma identidade exclusiva e imutável (chave de endosso) que pode ser usada para identificar um determinado computador. Os TPMs também medem o processo de inicialização do computador, armazenando hashes de medidas sensíveis à segurança em PCRs (Registros de Controle de Plataforma) que podem ser lidos, mas não modificados pelo sistema operacional. Essas medidas são usadas durante o atestado para fornecer prova de criptografia de que um computador está na configuração de segurança que alega estar. |
| Chave de host | O atestado de chave de host é uma forma mais simples de atestado que verifica apenas a identidade de um computador usando um par de chaves assimétricas. A chave privada é armazenada no computador que executa o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e a chave pública é fornecida para o HGS. A configuração de segurança do computador não é medida e um chip TPM 2.0 não é necessário no computador que executa o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]. É importante proteger a chave privada instalada no computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] porque qualquer pessoa que obtiver essa chave pode representar um computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] legítimo e o enclave VBS em execução dentro de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]. |

Em geral, fazemos as seguintes recomendações:

- Para **servidores de produção físicos**, é recomendável usar o atestado do TPM para obter as garantias adicionais que ele fornece.
- Para **servidores de produção virtuais**, recomendamos o atestado de chave de host, pois a maioria das máquinas virtuais não tem TPMs virtuais ou Inicialização Segura. Se você estiver usando uma VM com segurança aprimorada como uma [VM blindada no local](/windows-server/security/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms-top-node), poderá optar por usar o modo TPM. Em todas as implantações virtualizadas, o processo de atestado apenas analisa seu ambiente de VM, não a plataforma de virtualização sob a VM.
- Para **cenários de desenvolvimento/teste**, recomendamos o atestado de chave de host porque é mais fácil de configurar.

### <a name="trust-model"></a>Modelo de confiança

No modelo de confiança de enclave VBS, as consultas e os dados criptografados são avaliados em um enclave baseado em software para protegê-lo do sistema operacional host.
O acesso a esse enclave é protegido pelo hipervisor da mesma maneira que duas máquinas virtuais em execução no mesmo computador não podem acessar a memória uma da outra.
Para que um cliente confie que está se comunicando com uma instância legítima do VBS, você deve usar o atestado baseado em TPM que estabelece uma raiz de hardware de confiança no computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].
As medidas do TPM capturadas durante o processo de inicialização incluem a chave de identidade exclusiva da instância do VBS, garantindo que o certificado de integridade seja válido apenas nesse computador.
Além disso, quando um TPM está disponível em um computador que executa o VBS, a parte privada da chave de identidade do VBS é protegida pelo TPM, impedindo que alguém tente representar essa instância de VBS.

A inicialização segura é necessária com o atestado do TPM para garantir que a UEFI carregou um carregador de inicialização legítimo, assinado pela Microsoft e que nenhum rootkit interceptou o processo de inicialização do hipervisor.
Além disso, um dispositivo IOMMU é necessário por padrão para garantir que os dispositivos de hardware com acesso direto à memória não possam inspecionar ou modificar a memória do enclave.

Essas proteções pressupõem que o computador que executa o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] é um computador físico.
Se virtualizar o computador que executa o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], você não poderá mais garantir que a memória da VM esteja segura contra inspeção pelo administrador do hipervisor ou pelo hipervisor. Um administrador de hipervisor poderia, por exemplo, despejar a memória da VM e obter acesso à versão de texto não criptografado da consulta e dos dados no enclave.
Da mesma forma, mesmo que a VM tenha um TPM virtual, ela só pode medir o estado e a integridade do sistema operacional da VM e do ambiente de inicialização.
Ela não pode medir o estado do hipervisor que controla a VM.

No entanto, mesmo quando [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] é virtualizado, o enclave ainda é protegido contra ataques originados no sistema operacional da VM.
Se você confiar em seu hipervisor ou no provedor de nuvem e estiver preocupado principalmente com o administrador do banco de dados e ataques de administrador do sistema operacional em relação a informações confidenciais, um [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] virtualizado poderá atender aos seus requisitos.

Da mesma forma, o atestado de Chave de Host ainda é valioso em situações em que um módulo do TPM 2.0 não está instalado no computador que executa o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] ou em cenários de desenvolvimento/teste em que a segurança não é fundamental.
Você ainda pode usar muitos dos recursos de segurança mencionados acima, incluindo Inicialização Segura e um módulo do TPM 1.2, para proteger melhor o VBS e o sistema operacional como um todo.
Mas, como não há como o HGS verificar se o computador realmente tem essas configurações habilitadas com o atestado de Chave de Host, o cliente não tem garantia de que o host está realmente usando todas as proteções disponíveis.

## <a name="prerequisites"></a>Pré-requisitos

### <a name="hgs-server-prerequisites"></a>Pré-requisitos do servidor do HGS

Os computadores que executam a função de Serviço Guardião de Host devem atender aos seguintes requisitos:

| Componente | Requisito |
| --------- | ----------- |
| Sistema operacional | Windows Server 2019 edição Standard ou Datacenter |
| CPU | 2 núcleos (mínimo), 4 núcleos (recomendado) |
| RAM | 8 GB (mínimo) |
| NICs | Dois NICs com IPs estáticos recomendados (um para o tráfego de cluster, um para o serviço HGS) |

O HGS é uma função associada à CPU devido ao número de ações que exigem criptografia e descriptografia.
O uso de processadores modernos com recursos de aceleração criptográfica melhorará o desempenho do HGS.
Os requisitos de armazenamento para os dados de atestado são mínimos, no intervalo de 10 KB a 1 MB por atestado de computador exclusivo.

O computador do HGS não deve ser ingressado em um domínio antes de você começar.

### <a name="ssnoversion-md-computer-prerequisites"></a>Pré-requisitos do computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]

Os computadores em execução [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] devem atender aos [Requisitos de instalação do SQL Server](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md) e aos [Requisitos de hardware do Hyper-V](/virtualization/hyper-v-on-windows/reference/hyper-v-requirements#hardware-requirements).

Estes requisitos incluem:

- [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)] ou posterior
- Windows 10 Enterprise versão 1809 ou posterior; ou Windows Server 2019 Datacenter Edition. Outras edições do Windows 10 e do Windows Server não dão suporte a atestado com HGS.
- Suporte de CPU para tecnologias de virtualização:
  - Intel VT-x com Tabelas de Página Estendida.
  - AMD-V com Indexação de Virtualização Rápida.
  - Se você estiver executando [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] em uma VM, o hipervisor e a CPU física deverão oferecer recursos de virtualização aninhados. Confira a seção [modelo de confiança](#trust-model) para obter informações sobre as garantias ao executar os enclaves VBS em uma VM.
    - No Hyper-V 2016 ou posterior, [habilite as extensões de virtualização aninhadas no processador da VM](/virtualization/hyper-v-on-windows/user-guide/nested-virtualization#configure-nested-virtualization).
    - No Azure, selecione um tamanho de VM que dê suporte à virtualização aninhada. Todas as VMs da série v3 são compatíveis com virtualização aninhada, por exemplo, Dv3 e Ev3. Confira [Criar uma VM do Azure compatível com aninhamento](/azure/virtual-machines/windows/nested-virtualization#create-a-nesting-capable-azure-vm).
    - No VMware vSphere 6.7 ou posterior, habilite o suporte de segurança baseada em virtualização para a VM conforme descrito na [documentação do VMware](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.vm_admin.doc/GUID-C2E78F3E-9DE2-44DB-9B0A-11440800AADD.html).
    - Outros hipervisores e nuvens públicas podem dar suporte a recursos de virtualização aninhados que também permitem Always Encrypted com enclaves de VBS. Verifique a documentação da solução de virtualização para obter instruções sobre compatibilidade e configuração.
- Se você planeja usar o atestado de TPM, precisará de um chip TPM 2.0 Rev 1.16 pronto para uso no servidor. Neste momento, o atestado HGS não funciona com chips TPM 2.0 Rev 1.38. Além disso, o TPM deve ter um Certificado de Chave de Endosso válido.

## <a name="roles-and-responsibilities-when-configuring-attestation-with-hgs"></a>Funções e responsabilidades ao configurar o atestado com o HGS

A configuração do atestado com o HGS envolve a configuração de componentes de tipos diferentes: HGS, computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], instâncias de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e aplicativos que disparam o atestado do enclave. A configuração de componentes de cada tipo é executada por usuários supondo uma das funções distintas abaixo:

- Administrador do HGS – implanta o HGS, registra computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] com HGS e compartilha a URL de atestado do HGS com administradores de computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e administradores de aplicativos cliente.
- Administrador do computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] – instala os componentes cliente do atestado, habilita VBS em computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], fornece ao administrador do HGS as informações necessárias para registrar os computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] com o HGS, configura a URL de atestado em computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e verifica se os computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] podem atestar com êxito com o HGS.
- DBA – configura enclaves seguros em instâncias de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)].
- Administrador de aplicativos – configura o aplicativo com a URL de atestado obtida do administrador do HGS.

Em ambientes de produção (manipulando dados confidenciais reais), é importante que sua organização obedeça à separação de funções ao configurar o atestado, em que cada função distinta é assumida por pessoas diferentes. Em particular, se a meta da implantação de Always Encrypted em sua organização é reduzir a área da superfície de ataque ao garantir que administradores de computadores [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e DBAs não possam acessar dados confidenciais, administradores de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e DBAs não devem controlar os servidores do HGS.

## <a name="devtest-environment-considerations"></a>Considerações de ambiente de Desenvolvimento/Teste

Se estiver usando o Always Encrypted com enclaves VBS em um ambiente de desenvolvimento ou teste e não exigir alta disponibilidade ou proteção forte do computador que executa o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], você poderá fazer uma ou todas as seguintes concessões para uma implantação simplificada:

- Implante apenas um nó do HGS. Embora o HGS instale um cluster de failover, você não precisará adicionar mais nós se a alta disponibilidade não for uma preocupação.
- Use o modo de chave de host em vez do modo TPM para uma experiência de configuração mais simples.
- Virtualize o HGS e/ou o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para economizar recursos físicos.
- Execute o SSMS ou outras ferramentas para configurar o Always Encrypted com enclaves seguros no mesmo computador que [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]. Isso deixa as chaves mestras de coluna no mesmo computador que [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)], portanto, não faça isso em um ambiente de produção.

## <a name="next-steps"></a>Próximas etapas

- [Implantar o Serviço Guardião de Host para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]](./always-encrypted-enclaves-host-guardian-service-deploy.md)