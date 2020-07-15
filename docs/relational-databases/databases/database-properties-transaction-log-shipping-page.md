---
title: Propriedades de banco de dados (página Envio de Logs de Transações) | Microsoft Docs
description: Use a guia Envio de Logs de Transação na caixa de diálogo Propriedades do Banco de Dados para habilitar um banco de dados como um banco de dados primário de envio de logs e definir suas opções.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.logshipping.f1
ms.assetid: 72c4e539-fe11-4d57-b977-65b418d5916f
author: stevestein
ms.author: sstein
ms.openlocfilehash: 75c87efd24b1e345cb99413d1a524e872f0eb022
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85630967"
---
# <a name="database-properties-transaction-log-shipping-page"></a>Propriedades de banco de dados (página Envio do Logs de Transações)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use essa página para configurar e modificar as propriedades de envio de logs para um banco de dados.  
  
 Para obter uma explicação dos conceitos de envio de log, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opções  
 **Habilitar como banco de dados primário em uma configuração de envio de logs**  
 Habilita esse banco de dados como banco de dados primário para envio de logs. Selecione-o e, em seguida, configure as opções restantes na página. Se você desmarcar essa caixa de seleção, a configuração de envio de logs será descartada para esse banco de dados.  
  
 **Configurações de Backup**  
 Clique em **Configurações de Backup** para configurar o agendamento de backup, local, alerta e parâmetros de arquivamento.  
  
 **Agenda do Backup**  
 Mostra a agenda de backup selecionada presentemente para o banco de dados primário. Clique em **Configurações de Backup** para modificar essas configurações.  
  
 **Último Backup Criado**  
 Indica hora e data do último backup de log da transação do banco de dados primário.  
  
 **Instâncias e bancos de dados do servidor secundário**  
 Lista os servidores secundários presentemente configurados e os bancos de dados desse banco de dados primário. Destaque um banco de dados e depois clique em **...** para modificar os parâmetros associados àquele banco de dados secundário.  
  
 **Adicionar**  
 Clique em **Adicionar** para adicionar um banco de dados secundário à configuração de envio de logs para esse banco de dados primário.  
  
 **Remover**  
 Remove um banco de dados selecionado dessa configuração de envio de logs. Selecione primeiramente o banco de dados, depois clique em **Remover**.  
  
 **Use uma instância do servidor monitor**  
 Define uma instância de servidor monitor para essa configuração de envio de logs. Marque a caixa de seleção **Usar uma Instância de Servidor Monitor** , depois clique em **Configurações** para especificar a instância de servidor monitor.  
  
 **Instância de Servidor Monitor**  
 Indica a instância de servidor monitor atualmente configurada para essa configuração de envio de logs.  
  
 **Configurações**  
 Configura a instância de servidor monitor para uma configuração de envio de logs. Clique em **Configurações** para configurar essa instância de servidor monitor.  
  
 **Configuração do Script**  
 Gera um script para configuração do envio de logs com os parâmetros selecionados. Clique em **Configuração do script**, depois selecione um destino de saída para o script.  
  
> [!IMPORTANT]  
>  Antes de gerar scripts de configurações para um banco de dados secundário, é preciso chamar a caixa de diálogo **Configurações do Banco de Dados Secundário** . Chamar essa caixa de diálogo conecta você ao servidor secundário e recupera as configurações atuais do banco de dados secundário que são necessárias para gerar o script.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de envio de logs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)   
 [Tabelas de envio de logs &#40;Transact-SQL&#41;](../../relational-databases/system-tables/log-shipping-tables-transact-sql.md)  
  
  
