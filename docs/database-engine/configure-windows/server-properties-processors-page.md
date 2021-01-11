---
title: Propriedades do Servidor (página de processadores)
description: Familiarize-se com as configurações do processador no SQL Server. Saiba quais opções controlam o número de threads de trabalho, a atribuição de processador e outras propriedades.
ms.prod: sql
ms.prod_service: high-availability
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
author: markingmyname
ms.author: maghan
ms.reviewer: drskwier, matteot
ms.custom: ''
ms.date: 12/17/2020
ms.openlocfilehash: 874cbbae2b418e9b9e06c7a95d62d34a99af38f5
ms.sourcegitcommit: a81823f20262227454c0b5ce9c8ac607aaf537e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97684212"
---
# <a name="server-properties-processors-page"></a>Propriedades do Servidor (página Processadores)

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Use esta página para exibir ou modificar suas opções de processador. As configurações de afinidade do processador só são habilitadas quando há mais de um processador instalado.  

## <a name="options"></a>Opções

### <a name="processor-affinity"></a>Afinidade do Processador
Atribui processadores a threads específicos para eliminar recargas do processador e reduzir a migração de thread pelos processadores. Para obter mais informações, veja [Opção affinity mask de configuração de servidor](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md).

### <a name="io-affinity"></a>Afinidade de E/S
Associa a E/S de disco do SQL Server [!INCLUDE[msCoName](../../includes/msconame-md.md)] a um subconjunto especificado de CPUs. Para obter mais informações, veja [Opção affinity Input-Output mask de configuração de servidor](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md).

### <a name="automatically-set-processor-affinity-mask-for-all-processors"></a>Definir automaticamente a máscara de afinidade de todos os processadores
Permite que o SQL Server defina a afinidade do processador.

### <a name="automatically-set-io-affinity-mask-for-all-processors"></a>Definir automaticamente a máscara de afinidade de E/S de todos os processadores
Permite que o SQL Server defina a afinidade de E/S.

### <a name="maximum-worker-threads"></a>Máximo de threads de trabalho
0 permite que o SQL Server defina dinamicamente o número de threads de trabalho. Essa configuração é melhor para a maioria dos sistemas. Porém, dependendo de sua configuração de sistema, definir essa opção com um valor específico às vezes melhora o desempenho. Para obter mais informações, consulte [configurar a opção de configuração de servidor max worker threads](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md).  

### <a name="boost-sql-server-priority"></a>Aumentar a prioridade do SQL Server
Especifica se o SQL Server deve ser executado em uma prioridade de agendamento do Microsoft Windows mais alta que outros processos no mesmo computador. Para obter mais informações, consulte [Configure the priority boost Server Configuration Option](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md).  

> [!Note]
> Essa opção não está disponível no SSMS 18.x e em versões posteriores.

### <a name="use-windows-fibers-lightweight-pooling"></a>Usar fibras do Windows (lightweight pooling)
Use fibras do Windows em vez de threads no serviço do SQL Server. Isso só está disponível no Windows 2003 Server Edition. Para saber mais, veja [lightweight pooling Server Configuration Option](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md).

> [!Note]
> Essa opção não está disponível no SSMS 18.x e em versões posteriores.

### <a name="configured-values"></a>Valores Configurados
Exibe os valores configurados para as opções nesse painel. Se você alterar esses valores, selecione **Executando Valores** para verificar se as alterações entraram em vigor. Se não tiverem entrado, a instância do SQL Server deverá ser reiniciada.

### <a name="running-values"></a>Executando Valores
Exiba os valores que estão sendo executados para as opções neste painel. Esses valores são somente leitura.

## <a name="see-also"></a>Consulte Também
[Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  


