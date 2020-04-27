---
title: Configurar a opção de configuração de servidor cursor threshold | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- cursor threshold option
ms.assetid: 189f2067-c6c4-48bd-9bd9-65f6b2021c12
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a710ef8474ea0ce67d0b549febb3a9dd40aa36e0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62811367"
---
# <a name="configure-the-cursor-threshold-server-configuration-option"></a>Configurar a opção de configuração de servidor cursor threshold
  Este tópico descreve como configurar a opção de configuração de servidor **cursor threshold** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **cursor threshold** especifica o número de linhas no conjunto de cursores em que os conjuntos de chaves de cursor são gerados de forma assíncrona. Quando os cursores geram um conjunto de chaves para um conjunto de resultados, o otimizador de consulta calcula o número de linhas que serão retornadas para aquele conjunto de resultados. Se o otimizador de consulta calcular que o número de linhas retornadas é maior do que esse limite, o cursor será gerado de forma assíncrona, permitindo que o usuário busque linhas do cursor enquanto o cursor continua sendo populado. Caso contrário, o cursor é gerado de forma síncrona e a consulta aguarda até que todas as linhas sejam retornadas.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção cursor threshold usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção cursor threshold](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não dá suporte à geração de cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] controlados por conjunto de chaves ou estáticos de forma assíncrona. [!INCLUDE[tsql](../../includes/tsql-md.md)] , como OPEN ou FETCH, são em lote, de modo que não é preciso gerar cursores [!INCLUDE[tsql](../../includes/tsql-md.md)] assincronamente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] continua a dar suporte a cursores de servidor de API (interface de programação de aplicativo) estáticos ou controlados por conjunto de chaves assíncronos nos quais OPEN de baixa latência é uma preocupação devido às viagens de ida e volta do cliente para cada operação de cursor.  
  
-   A exatidão do otimizador de consulta para determinar uma estimativa do número de linhas em um conjunto de chaves depende da moeda das estatísticas para cada tabela no cursor.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Esta é uma opção avançada e deve ser alterada somente por um administrador de banco de dados experiente ou técnico certificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Se você definir o **cursor threshold** como -1, todos os conjuntos de chaves serão gerados de forma síncrona, o que beneficiará pequenos conjuntos de cursores. Se você definir o **cursor threshold** como 0, todos os conjuntos de chaves serão gerados de forma assíncrona. Com outros valores, o otimizador de consulta irá comparar o número de linhas previstas no cursor definido e criará o conjunto de chaves de forma assíncrona se ele exceder o número definido em **cursor threshold**. Não defina **cursor threshold** com um valor muito baixo, pois conjuntos de resultados pequenos são criados melhor de forma síncrona.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>Para configurar a opção cursor threshold  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Avançado** .  
  
3.  Em **Diversos**, altere a opção **Limite do Cursor** para o valor desejado.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-cursor-threshold-option"></a>Para configurar a opção cursor threshold  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) para definir a opção `cursor threshold` como `0` para que os conjuntos de chaves dos cursores sejam gerados de forma assíncrona.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'cursor threshold', 0 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 Para obter mais informações, veja [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md).  
  
##  <a name="follow-up-after-you-configure-the-cursor-threshold-option"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar a opção cursor threshold  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [@@CURSOR_ROWS &#40;Transact-SQL&#41;](/sql/t-sql/functions/cursor-rows-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)  
  
  
