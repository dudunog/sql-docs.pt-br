---
title: Exibir o estado de um banco de dados espelhado (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- states [SQL Server], database mirroring
- database mirroring [SQL Server], states
ms.assetid: 544f4194-253e-4c57-96ca-31c16301434f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 7a6d664a838e82a10df4ab16f4f6c097ffacf8b2
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933804"
---
# <a name="view-the-state-of-a-mirrored-database-sql-server-management-studio"></a>Exibir o estado de um banco de dados espelho (SQL Server Management Studio)
  Durante uma sessão de espelhamento de banco de dados, você pode exibir o estado na página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** .  
  
### <a name="to-view-the-status-of-a-database-mirroring-session"></a>Para exibir o estado de uma sessão de espelhamento de banco de dados  
  
1.  Depois de se conectar à instância do servidor principal, no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda os **Bancos de Dados**e selecione o banco de dados a ser espelhado.  
  
3.  Clique com o botão direito do mouse no banco de dados, selecione **Tarefas**e clique em **Espelhar**. Isso abre a página **Espelhamento** da caixa de diálogo **Propriedades do Banco de Dados** .  
  
4.  Depois do início do espelhamento, o painel **Status** exibe o status da sessão de espelhamento de banco de dados a partir de quando você selecionou a página **Espelhamento** ou clicou o botão **Atualizar** . Os possíveis estados são os seguintes:  
  
    |Estados|Explicação|  
    |------------|-----------------|  
    |\<blank>|Não existe nenhuma sessão de espelhamento de banco de dados e não há nenhuma atividade a ser reportada na página **Espelhamento** .|  
    |Em Pausa|O banco de dados principal está em execução mas não está enviando nenhum log ao servidor espelho. A cópia espelhada do banco de dados não está disponível.|  
    |Nenhuma conexão|A instância do servidor principal não pode conectar com seu parceiro ou com a instância de servidor testemunha (se houver)|  
    |Sincronizando|O conteúdo do banco de dados espelho está ficando atrás do conteúdo do banco de dados principal. A instância do servidor principal está enviando registros de log para a instância do servidor espelho, a qual está aplicando as alterações ao banco de dados espelho para rolagem para frente.<br /><br /> Ao início de uma sessão de espelhamento de banco de dados, os bancos de dados espelho e principal encontram-se no estado de sincronização.|  
    |Failover|Na instância de servidor principal, um failover manual (troca de papel) começou mas ainda não foi aceito pelo espelho.|  
    |Sincronizado|O banco de dados espelho contém os mesmos dados que o banco de dados principal. Failover manuais e automáticos *apenas* são possíveis no estado sincronizado.|  
  
## <a name="see-also"></a>Consulte Também  
 [Estados de espelhamento &#40;SQL Server&#41;](mirroring-states-sql-server.md)  
  
  
