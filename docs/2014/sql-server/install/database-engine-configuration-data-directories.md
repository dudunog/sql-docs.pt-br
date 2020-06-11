---
title: Configuração de Mecanismo de Banco de Dados-diretórios de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 9b1fa0fc-623b-479a-afc3-4f13bd850487
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 641656bede6163e1630ef2b39c54ca931d8b6ec4
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83859719"
---
# <a name="database-engine-configuration---data-directories"></a>Configuração do Mecanismo de Banco de Dados – Diretórios de dados
  Use esta página para especificar o local de instalação para programas e arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]. Com base no tipo de instalação, o armazenamento com suporte pode incluir disco local, armazenamento compartilhado ou um servidor de arquivos SMB.  
  
 Para especificar um compartilhamento de arquivos SMB como um diretório, você deve digitar o caminho UNC com suporte manualmente. Não há suporte para a navegação até um compartilhamento de arquivos SMB. Este é um formato de caminho UNC de um compartilhamento de arquivos SMB com suporte: \\\NomeServidor\NomeCompartilhamento\\....  
  
## <a name="stand-alone-instance-of-ssnoversion"></a>Instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 A tabela a seguir lista os tipos de armazenamento com suporte e os diretórios padrão para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que podem ser configurados pelo usuário durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
  
|Description|Tipo de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Diretório raiz de dados|Disco local, servidor de arquivos SMB, armazenamento compartilhado <sup>1</sup>|C:\Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \| [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Setup irá configurar ACLs para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretórios e interromper a herança como parte da configuração.|  
|Diretório do banco de dados de usuário|Disco local, servidor de arquivos SMB, armazenamento compartilhado <sup>1</sup>|C:\Arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Data|As práticas recomendadas para diretórios de dados de usuário dependem dos requisitos de carga de trabalho e desempenho.|  
|Diretório de log do banco de dados de usuário|Disco local, servidor de arquivos SMB, armazenamento compartilhado <sup>1</sup>|C:\Arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Data|Verifique se o diretório de log tem espaço suficiente.|  
|Diretório de BD temporário|Disco local, servidor de arquivos SMB, armazenamento compartilhado <sup>1</sup>|C:\Arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Data|As práticas recomendadas para o diretório Temp dependem dos requisitos de carga de trabalho e desempenho.|  
|Diretório de log de BD temporário|Disco local, servidor de arquivos SMB, armazenamento compartilhado <sup>1</sup>|C:\Arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Data|Verifique se o diretório de log tem espaço suficiente.|  
|Diretório de backup|Disco local, servidor de arquivos SMB, armazenamento compartilhado <sup>1</sup>|C:\Arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Backup|Defina as permissões adequadas para evitar perda de dados e verifique se a conta de usuário para o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem permissões suficientes para realizar gravações no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
 <sup>1</sup> embora os discos compartilhados tenham suporte, não é uma prática recomendada para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="failover-cluster-instance-of-ssnoversion"></a>Instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 A tabela a seguir lista os tipos de armazenamento compatíveis e os diretórios padrão para uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são configuráveis pelo usuário durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Description|Tipo de armazenamento com suporte|Diretório Padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Diretório raiz de dados|Armazenamento compartilhado, servidor de arquivos SMB|\<Unidade:>\Arquivos de Programas\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.|  
|Diretório do banco de dados de usuário|Armazenamento compartilhado, servidor de arquivos SMB|\<Unidade: >arquivos de programas \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Data<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|As práticas recomendadas para diretórios de dados de usuário dependem dos requisitos de carga de trabalho e desempenho.|  
|Diretório de log do banco de dados de usuário|Armazenamento compartilhado, servidor de arquivos SMB|\<Unidade: > \Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Data<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|Verifique se o diretório de log tem espaço suficiente.|  
|Diretório de BD temporário|Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Unidade: > \Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Data<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|Verifique se o diretório especificado é válido para todos os nós de cluster. Durante o failover, se os diretórios tempdb não estiverem disponíveis no nó do destino de failover, o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não ficará online.|  
|Diretório de log de BD temporário|Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Unidade: > \Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Data<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|Verifique se o diretório especificado é válido para todos os nós de cluster. Durante o failover, se os diretórios tempdb não estiverem disponíveis no nó do destino de failover, o recurso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não ficará online.|  
|Diretório de backup|Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Unidade: > \Program Files \\ [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] \MSSQL12. \< InstanceID> \MSSQL\Backup<br /><br /> Dica: se o disco compartilhado tiver sido selecionado na página **Seleção de Disco de Cluster** , o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster** .|Defina as permissões adequadas para evitar perda de dados e verifique se a conta de usuário do serviço do SQL Server tem permissões suficientes para gravar no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
## <a name="security-considerations"></a>Considerações de segurança  
 A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.  
  
 As seguintes recomendações se aplicam ao servidor de arquivos SMB:  
  
-   A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser uma conta de domínio se for usado um servidor de arquivos SMB.  
  
-   A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter permissões NTFS FULL CONTROL na pasta de compartilhamento de arquivos SMB usada como o diretório de dados.  
  
-   A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter privilégios SeSecurityPrivilege no servidor de arquivos SMB. Para conceder esse privilégio, use o console de Política de Segurança Local no servidor de arquivos para adicionar a conta de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à política **Gerenciar o log de auditoria e segurança**. Essa configuração está disponível na seção **atribuições de direitos de usuário** em **políticas locais** no console de **política de segurança local** .  
  
## <a name="notes"></a>Observações  
  
-   Ao adicionar recursos a uma instalação existente, você não pode alterar o local de um recurso instalado anteriormente, nem especificar o local para um novo recurso.  
  
-   Se você especificar diretórios de instalação diferentes do padrão, assegure que as pastas de instalação sejam exclusivas a esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também devem ser instalados em diretórios separados.  
  
-   Os arquivos de programas e os arquivos de dados não podem ser instalados nas seguintes situações:  
  
    -   Em uma unidade de disco removível  
  
    -   Em um sistema de arquivos que usa compactação  
  
    -   Em um diretório onde os arquivos do sistema estão localizados  
  
    -   Em uma unidade de rede mapeada em uma instância de cluster de failover  
  
## <a name="see-also"></a>Consulte Também  
 [Locais de arquivos para instâncias padrão e nomeadas do SQL Server](../../../2014/sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [Permissões de compartilhamento e de NTFS em um servidor de arquivos](https://go.microsoft.com/fwlink/?LinkID=206571)  
  
  
