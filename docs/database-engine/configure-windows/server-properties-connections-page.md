---
title: Propriedades do servidor (página Conexões) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.connections.f1
ms.assetid: 33be8ac5-12dd-4b8a-99e0-68261c219dd2
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 15ab408465890a13fc6e87efd2f2e15e8f8a7fad
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68025493"
---
# <a name="server-properties---connections-page"></a>Propriedades do servidor – página Conexões
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use esta página para exibir ou modificar suas opções de conexão.  
  
## <a name="connections"></a>conexões  
 **Número máximo de conexões simultâneas (0 = ilimitado)**  
 Se definido como um valor diferente de zero, limita o número de conexões que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permitirá.  
  
> [!CAUTION]  
>  A definição para um valor pequeno, como 1 ou 2, pode impedir que os administradores se conectem para administrar o servidor; no entanto, a Conexão dedicada de administrador está sempre apta a se conectar.  
  
## <a name="default-connection-options"></a>Opções de conexão padrão  
 **Default connection options**  
 Especifica as opções de conexão padrão, como descrito na tabela a seguir.  
  
|Opções de configuração|Descrição|  
|--------------------------|-----------------|  
|**desabilite verificação de restrição adiada**|Controla a verificação provisória ou adiada de restrições.|  
|**transações implícitas**|Controla se uma transação é iniciada implicitamente ou não, quando uma instrução é executada.|  
|**fechar cursor ao confirmar**|Controla o comportamento de cursores depois que uma operação de confirmação foi executada.|  
|**avisos ansi**|Controla truncamento e NULL em avisos de agregação.|  
|**preenchimento ansi**|Controla o preenchimento de variáveis do comprimento fixo.|  
|**ansi nulls**|Controla o tratamento de `NULL` ao usar operadores de igualdade.|  
|**anular aritmética**|Encerra uma consulta quando ocorre estouro ou erro de divisão por zero durante a execução da consulta.|  
|**ignorar aritmética**|Retorna NULL quando ocorre estouro ou erro de divisão por zero, durante a consulta.|  
|**identificador entre aspas**|Faz a diferenciação entre aspas simples e duplas ao avaliar uma expressão.|  
|**sem contagem**|Desativa a mensagem retornada ao término de cada instrução que declara quantas linhas foram afetadas.|  
|**padrão ansi null ativado**|Altera o comportamento da sessão para usar a compatibilidade ANSI para nulidade. Novas colunas definidas sem a nulidade explícita são definidas para permitir nulos.|  
|**padrão ansi null desativado**|Altera o comportamento da sessão, para não usar a compatibilidade ANSI para nulidade. Novas colunas definidas sem a nulidade explícita são definidas para não permitir nulos.|  
|**concatenar nulo produz nulo**|Retorna NULL ao concatenar um valor NULL com uma cadeia de caracteres.|  
|**anular arredondamento numérico**|Gera um erro quando ocorre perda de precisão em uma expressão.|  
|**anular transação**|Reverte uma transação se uma instrução Transact-SQL ativar um erro em tempo de execução.|  
  
 Para obter mais informações sobre opções de conexão, pesquise sobre a opção específica nos Manuais Online.  
  
## <a name="remote-server-connections"></a>Conexões do servidor remoto  
 **Permitir conexões remotas com este servidor**  
 Controla a execução de procedimentos armazenados de servidores remotos que executam instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Marcar essa caixa de seleção tem o mesmo efeito que definir a opção **sp_configureremote access** como 1. Desmarcá-la evita a execução de procedimentos armazenados de um servidor remoto.  
  
 **Tempo limite de consulta remota (em segundos, 0 = sem tempo limite)**  
 Especifica quanto tempo (em segundos) uma operação remota pode levar antes que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] chegue ao tempo limite. O padrão é 600 segundos ou uma espera de 10 minutos.  
  
 **Requer transações distribuídas para comunicação servidor a servidor**  
 Protege as ações de um procedimento servidor-a-servidor por meio de uma transação do MS DTC (Coordenador de Transações Distribuídas da [!INCLUDE[msCoName](../../includes/msconame-md.md)] ). Para obter mais informações, consulte [configurar a opção de configuração de servidor remote proc trans](../../database-engine/configure-windows/configure-the-remote-proc-trans-server-configuration-option.md).  
  
## <a name="property-page-display-options"></a>Opções Property Page Display  
 **Valores Configurados**  
 Exibe os valores configurados para as opções nesse painel. Se você alterar esses valores, clique em **Executando Valores** para verificar se as alterações entraram em vigor. Se não houver nenhum, a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser reiniciada.  
  
 **Executando Valores**  
 Exiba os valores que estão sendo executados para as opções neste painel. Esses valores são somente leitura.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de &#40;execução da consulta: SQL Server: Página Avançada&#41;](https://msdn.microsoft.com/library/3ec788c7-22c3-4216-9ad0-81a168d17074)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
