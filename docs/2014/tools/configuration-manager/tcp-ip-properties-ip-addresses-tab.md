---
title: Propriedades de TCP-IP (guia endereços IP) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], listening on
- listening [SQL Server], on ports
ms.assetid: 4c17ed45-9da7-4bec-bce6-970109fe7365
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: afb62458cb76a1187dce06efadeca00fc8a382f2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63151442"
---
# <a name="tcp-ip-properties-ip-addresses-tab"></a>Propriedades de TCP-IP (guia endereços IP)
  Use a caixa de diálogo **Propriedades do TCP/IP (Guia Endereços IP)** para configurar as opções do protocolo TCP/IP de um endereço IP específico. Somente as **Portas TCP Dinâmicas** e a **Porta TCP** podem ser configuradas para todos os endereços de uma só vez com a seleção de **IP Tudo**.  
  
 As alterações entram em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vigor quando o é reiniciado. Para obter informações sobre como iniciar e parar o serviço do SQL Server Browser, consulte Como: Iniciar e parar o serviço SQL Server Browser nos Manuais Online.  
  
## <a name="static-vs-dynamic-ports"></a>Portas estáticas vs. Portas dinâmicas  
 A instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta as conexões de entrada na porta 1433. A porta pode ser alterada por razões de segurança ou por causa do requisito de um aplicativo cliente. Por padrão, instâncias nomeadas (inclusive do SQL Server Express) são configuradas para escutar em portas dinâmicas. Para configurar uma porta estática, deixe a caixa **Portas TCP Dinâmicas** em branco e forneça um número de porta disponível na caixa **Porta TCP** . Para obter mais informações sobre como abrir portas no firewall, consulte Configurando o firewall do Windows para permitir o acesso do SQL Server nos Manuais Online.  
  
## <a name="dynamic-ports"></a>Portas dinâmicas  
 Na inicialização, quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é configurada para escutar em portas dinâmicas, ela verifica no sistema operacional se existe uma porta disponível e abre um ponto de extremidade para essa porta. Esse número deve ser especificado pelas conexões de entrada. Como o número da porta pode ser alterado cada vez que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o Serviço Navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para monitorar as portas, e direciona as conexões de entrada para a porta atual dessa instância. O uso de portas dinâmicas complica a conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] por meio de um firewall, pois o número da porta pode ser alterado quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for reiniciado, o que requer alterações nas configurações do firewall. Para evitar problemas de conexão por meio de um firewall, configure o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para usar uma porta estática.  
  
## <a name="options"></a>Opções  
 **Ativo**  
 Indica que o endereço IP está ativo no computador. Não disponível para **IP Tudo**.  
  
 **Enabled**  
 Se a propriedade **Escutar Tudo** em **Propriedades do TCP/IP (Guia Protocolo)** for definida como **Não**, essa propriedade indicará ser o SQL Server está escutando no endereço IP. Se a propriedade **Escutar Tudo** em **Propriedades do TCP/IP (Guia Protocolo)** estiver definida como **Sim**, a propriedade será desconsiderada. Não disponível para **IP Tudo**.  
  
 **Endereço IP**  
 Exiba ou altere o endereço de IP usado por esta conexão. Lista o endereço IP usado pelo computador e o endereço de loopback IP, 127.0.0.1. Não disponível para **IP Tudo**. O endereço IP pode estar no formato IPv4 ou IPv6.  
  
 **Portas TCP Dinâmicas**  
 Em branco, se as portas dinâmicas não estiverem habilitadas. Para usar portas dinâmicas, defina como 0.  
  
 Para **IP Tudo**, exibe o número da porta dinâmica usada.  
  
 **Porta TCP**  
 Exiba ou altere a porta na qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escuta. Por padrão, a instância padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] escuta na porta 1433.  
  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] pode escutar em várias portas no mesmo endereço IP. Liste as portas, separadas por vírgulas, no formato 1433,1500,1501. Este campo é limitado a 2.047 caracteres.  
  
 Para configurar um único endereço IP para escutar em várias portas, o parâmetro **Escutar Tudo** também deve ser definido como **Não**, na **Guia Protocolos** da caixa de diálogo **Propriedades do TCP/IP**. Para obter mais informações, consulte "Como: Configurar o mecanismo de banco de dados para escutar em várias portas TCP" em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Manuais Online.  
  
## <a name="adding-or-removing-ip-addresses"></a>Adicionando ou removendo endereços IP  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager exibe os endereços IP que estavam disponíveis no momento em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi instalado. Os endereços IP disponíveis podem ser alterados quando placas de rede são adicionadas ou removidas, quando um endereço IP atribuído dinamicamente expira, quando a estrutura de rede é reconfigurada ou quando o local físico do computador é alterado, como quando um computador laptop se conecta à rede em um edifício diferente. Para alterar um endereço IP, edite a caixa **Endereço IP** e reinicie o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [Escolhendo um protocolo de rede](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)   
 [Criando uma cadeia de conexão válida usando IP TCP](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [SQL Server Browser Service](../../../2014/tools/configuration-manager/sql-server-browser-service.md)  
  
  
