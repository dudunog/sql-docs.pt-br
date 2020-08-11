---
title: Propriedades do TCP/IP (Guia Endereços IP)
description: Saiba como usar a guia Endereços IP da caixa de diálogo Propriedades do TCP/IP para configurar as opções do protocolo TCP/IP de um endereço IP específico no SQL Server.
ms.custom: seo-lt-2019
ms.date: 08/24/2016
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- ports [SQL Server], listening on
- listening [SQL Server], on ports
ms.assetid: 4c17ed45-9da7-4bec-bce6-970109fe7365
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c68b7a9f1da65862403750e32315ee7168ded6e6
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880303"
---
# <a name="tcpip-properties-ip-addresses-tab"></a>Propriedades do TCP/IP (Guia Endereços IP)
[!INCLUDE [SQL Server Windows Only - ASDBMI ](../../includes/applies-to-version/sql-windows-only-asdbmi.md)]
  Use a caixa de diálogo **Propriedades do TCP/IP (Guia Endereços IP)** para configurar as opções do protocolo TCP/IP de um endereço IP específico. Somente as **Portas TCP Dinâmicas** e a **Porta TCP** podem ser configuradas para todos os endereços de uma só vez com a seleção de **IP Tudo**.  
  
 As alterações terão efeito quando o SQL Server for reiniciado. Para obter informações sobre como iniciar e interromper o serviço SQL Server Browser, consulte [Iniciar e interromper o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md).  
  
## <a name="static-vs-dynamic-ports"></a>Portas estáticas vs. Portas dinâmicas  
 A instância padrão do SQL Server escuta as conexões de entrada na porta 1433. A porta pode ser alterada por razões de segurança ou por causa do requisito de um aplicativo cliente. Por padrão, instâncias nomeadas (inclusive do SQL Server Express) são configuradas para escutar em portas dinâmicas. Para configurar uma porta estática, deixe a caixa **Portas TCP Dinâmicas** em branco e forneça um número de porta disponível na caixa **Porta TCP** . Para obter mais informações sobre como abrir portas no firewall, consulte Configurando o firewall do Windows para permitir o acesso do SQL Server nos Manuais Online.  
  
## <a name="dynamic-ports"></a>Portas dinâmicas  
 Na inicialização, quando uma instância do SQL Server é configurada para escutar em portas dinâmicas, ela verifica no sistema operacional se existe uma porta disponível e abre um ponto de extremidade para essa porta. Esse número deve ser especificado pelas conexões de entrada. Como o número da porta pode ser alterado sempre que o SQL Server é iniciado, o SQL Server fornece o Serviço SQL Server Browser para monitorar as portas, e direciona as conexões de entrada para a porta atual dessa instância. O uso de portas dinâmicas complica a conexão do SQL Server por meio de um firewall, pois o número da porta poderá ser alterado quando o SQL Server for reiniciado, o que exige alterações nas configurações do firewall. Para evitar problemas de conexão por meio de um firewall, configure o SQL Server para usar uma porta estática.  
  
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
 Exiba ou altere a porta de escuta do SQL Server. Por padrão, a instância padrão do SQL Server escuta na porta 1433.  
  
 O mecanismo de banco de dados pode escutar em várias portas no mesmo endereço IP. Liste as portas, separadas por vírgula, no formato 1433,1500,1501. Este campo é limitado a 2.047 caracteres.  
  
 Para configurar um único endereço IP para escutar em várias portas, o parâmetro **Escutar Tudo** também deve ser definido como **Não**, na **Guia Protocolos** da caixa de diálogo **Propriedades do TCP/IP**. Para saber mais, confira "Como: Configurar o mecanismo de banco de dados para escutar em várias portas TCP" em Manuais Online do SQL Server.  
  
## <a name="adding-or-removing-ip-addresses"></a>Adicionando ou removendo endereços IP  
 O SQL Server Configuration Manager exibe os endereços IP que estavam disponíveis no momento em que o SQL Server foi instalado. Os endereços IP disponíveis podem ser alterados quando placas de rede são adicionadas ou removidas, quando um endereço IP atribuído dinamicamente expira, quando a estrutura de rede é reconfigurada ou quando o local físico do computador é alterado, como quando um computador laptop se conecta à rede em um edifício diferente. Para alterar um endereço IP, edite a caixa **Endereço IP** e reinicie o SQL Server.  
  
## <a name="additional-topics-in-books-online"></a>Tópicos adicionais nos Manuais Online  
 Pesquise no MSDN tópicos como **Configurar um servidor para escuta em uma porta TCP específica (SQL Server Configuration Manager)** e **Configurar o Mecanismo de Banco de Dados para escuta em várias portas TCP**.  
  
## <a name="see-also"></a>Consulte Também  
 [Escolhendo um protocolo de rede](https://msdn.microsoft.com/library/ms187892(v=sql.120).aspx)   
 [Criando uma cadeia de conexão válida usando TCP/IP](creating-a-valid-connection-string-using-tcp-ip.md)   
 [Serviço Navegador do SQL Server](sql-server-browser-service.md)  
  
  
