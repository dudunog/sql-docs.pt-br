---
title: Configurar a opção de configuração de servidor index create memory | Microsoft Docs
description: Confira como usar a opção index create memory para definir a quantidade máxima de memória alocada inicialmente pelo SQL Server para as operações de classificação ao criar índices.
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- index create memory option
ms.assetid: 3d722d9b-bada-4bf5-a9d7-bfc556bb4915
author: markingmyname
ms.author: maghan
ms.openlocfilehash: afe6724ebac116e091072ab74ee37142a2ab8230
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85697204"
---
# <a name="configure-the-index-create-memory-server-configuration-option"></a>Configurar a opção de configuração de servidor index create memory
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **index create memory** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **index create memory** controla a quantidade máxima de memória alocada inicialmente para as operações de classificação ao criar índices. O valor padrão dessa opção é 0 (autoconfigurável). Se mais tarde for preciso mais memória para criação de índice e a memória estiver disponível, o servidor irá usá-la, excedendo assim a configuração dessa opção. Se a memória adicional não estiver disponível, a criação de índice continuará usando a memória já alocada.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção index create memory usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção index create memory](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   A configuração da opção **[min memory per query](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md)** tem precedência sobre a opção **index create memory**. Quando ambas as opções são alteradas, e a **index create memory** é inferior à **min memory per query**, você recebe uma mensagem de aviso, mas o valor foi definido. Durante a execução de consulta, você recebe um aviso semelhante.  
  
-   Ao usar tabelas e índices particionados, os requisitos mínimos de memória para criação de índice podem aumentar significativamente se houver índices particionados não alinhados e um alto grau de paralelismo. Essa opção controla a quantidade inicial total de memória alocada para todas as partições de índice em uma única operação de criação de índice. A consulta terminará com uma mensagem de erro se a quantidade definida por essa opção for inferior ao mínimo exigido para a execução da consulta.  
  
-   O valor de execução para essa opção não excederá a quantidade real de memória que pode ser usada pelo sistema operacional e pela plataforma de hardware nas quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executado.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou por um profissional de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] certificado.  
  
-   A opção **memória de criação de índice** é autoconfigurável e, normalmente, opera sem necessidade de ajustes. Porém, se você tiver dificuldade para criar índices, considere aumentar o valor dessa opção a partir de seu valor de execução.  

-   Criar um índice em um sistema de produção é, normalmente, uma tarefa realizada com pouca frequência e, muitas vezes, agendada como trabalho a executar fora do horário de pico. Portanto, ao criar índices com pouca frequência e fora do horário de pico, o aumento de **index create memory** pode melhorar o desempenho de criação de índice. Mantenha, contudo, a opção de configuração **[min memory per query](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md)** em um número menor, para que o trabalho de criação de índice seja iniciado ainda que a memória solicitada não esteja disponível.
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-index-create-memory-option"></a>Para configurar a opção index create memory  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Memória** .  
  
3.  Em **Memória de criação de índice**, digite ou selecione o valor desejado para a opção index create memory.  
  
     Use a opção **index create memory** para controlar a quantidade de memória usada por classificações de criação de índice. A opção **memória de criação de índice** é autoconfigurável e deve funcionar na maioria dos casos sem necessidade de ajustes. Porém, se você tiver dificuldade para criar índices, considere aumentar o valor dessa opção a partir de seu valor de execução. Classificações de consulta são controladas pela opção **min memory per query** .  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-index-create-memory-option"></a>Para configurar a opção index create memory  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para definir o valor da opção `index create memory` como `4096`.  
  
```sql  
USE AdventureWorks2012 ;  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
EXEC sp_configure 'index create memory', 4096  
GO  
RECONFIGURE;  
GO  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
##  <a name="follow-up-after-you-configure-the-index-create-memory-option"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar a opção index create memory  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [sys.configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-configurations-transact-sql.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções Server Memory de configuração do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
