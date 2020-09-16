---
description: Reservas de URL para várias instâncias de implantações do Servidor de Relatório
title: Reservas de URL para implantações de várias instâncias do Servidor de Relatório | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: f67c83c0-1f74-42bb-bfc1-e50c38152d3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 661dc1ee0e259cc2f1457e555ca685e8e581dc0e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88445958"
---
# <a name="url-reservations-for-multi-instance-report-server-deployments"></a>Reservas de URL para várias instâncias de implantações do Servidor de Relatório
  Se você instalar várias instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no mesmo computador, será preciso considerar como definirá as reservas de URL para cada instância. Em cada instância, o serviço Web do Servidor de Relatórios e o [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] devem ter, pelo menos, uma reserva de URL cada. O conjunto inteiro de reservas deve ser exclusivo em HTTP.SYS.  
  
 As URLs duplicadas são detectadas durante o registro de URL, que ocorre quando o serviço é iniciado. Se você criar reservas de URL que não forem exclusivas, o conflito de nome talvez não seja detectado até a inicialização do serviço Por esse motivo, certifique-se de que você segue as regras ou as convenções de nomenclatura para garantir que todos os valores são exclusivos.  
  
## <a name="default-naming-conventions"></a>Convenções de nomenclatura padrão  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode ser instalado em uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando você instala ou configura um servidor de relatório em uma instância nomeada, o nome da instância é incluído automaticamente no diretório virtual da reserva de URL padrão fornecida pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . A tabela a seguir mostra as reservas de URL de uma instância padrão e uma instância nomeada.  
  
|Instância do SQL Server|Reserva de URL padrão|  
|-------------------------|-----------------------------|  
|Padrão (MSSQLServer)|`https://+:80/reportserver`|  
|Nomeado (MynamedInstance)|`https://+:80/reportserver_MyNamedInstance`|  
  
 Para a instância nomeada, o diretório virtual inclui o nome da instância. Tanto a instância padrão quanto a instância nomeada escutam na mesma porta, mas os nomes exclusivos de diretório virtual determinam qual servidor de relatório obterá a solicitação.  
  
 Uma sugestão de prática recomendada é usar o nome do diretório virtual para fazer a distinção entre a instância do servidor de relatório. Isso fornece uma correspondência clara entre a URL e a instância de destino e garante que os nomes do aplicativo sejam exclusivos em todo o sistema.  
  
## <a name="custom-naming-conventions"></a>Convenções de nomenclatura personalizadas  
 Embora o uso da instância nomeada seja recomendado, você pode usar a sintaxe de URL e suas próprias convenções de nomenclatura para atender as restrições exclusivas de nome para as reservas de URL. Os exemplos a seguir ilustram diferentes abordagens para a criação das URLs exclusivas de cada instância.  
  
|Instância padrão do Servidor de Relatório (MSSQLSERVER)|ReportServer_MyNamedInstance|Exclusividade|  
|----------------------------------------------------|-----------------------------------|----------------|  
|`https://+:80/reportserver`|`https://+:8888/reportserver`|Cada instância escuta em uma porta diferente.|  
|`https://www.contoso.com/reportserver`|`https://SRVR-46/reportserver`|Cada instância responde a nomes de servidores diferentes (nome de domínio totalmente qualificado e nome de máquina).|  
  
## <a name="uniqueness-requirements"></a>Requisitos de exclusividade  
 As tecnologias subjacentes usadas pelo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] impõem requisitos aos nomes exclusivos. HTTP.SYS exige que todas as URLs do repositório sejam exclusivas. Você pode variar a porta, o nome de host ou o nome de diretório virtual para criar uma URL exclusiva. [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] exige que as identidades de aplicativo sejam exclusivas no mesmo processo. Esse requisito afeta os nomes do diretório virtual. Ele especifica que não é possível duplicar um nome de diretório virtual na mesma instância do servidor de relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar uma URL &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
