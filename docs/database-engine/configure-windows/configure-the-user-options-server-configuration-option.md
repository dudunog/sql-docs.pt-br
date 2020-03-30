---
title: Configurar a opção de configuração de servidor user options | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- global default for all users [SQL Server]
- users [SQL Server], global defaults
- user options option [SQL Server]
ms.assetid: cfed8f86-6bcf-4b90-88eb-9656e22d5dc5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d06cb92287537293739fa9bd7b1a86ea7ffd767a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68012158"
---
# <a name="configure-the-user-options-server-configuration-option"></a>Configurar as opções de configuração de servidor user connections
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Este tópico descreve como configurar a opção de configuração de servidor **user options** no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. A opção **user options** especifica padrões globais para todos os usuários. Uma lista de opções de processamento de consulta padrão é definida para a duração da sessão de trabalho de um usuário. A opção **user options** permite alterar os valores padrão das opções SET (se as configurações padrão do servidor não forem apropriadas).  
  
 Um usuário pode substituir esses padrões usando a instrução SET. Você pode configurar **user options** dinamicamente para novos logons. Depois de alterar a configuração de **user options**, novas sessões de logon usam a nova configuração; sessões de logon atuais não são afetadas.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para configurar a opção de configuração user options usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar a opção user options configuration](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   A tabela a seguir lista e descreve os valores de configuração para **user options**. Nem todos os valores de configuração são compatíveis entre si. Por exemplo, ANSI_NULL_DFLT_ON e ANSI_NULL_DFLT_OFF não podem ser definidas ao mesmo tempo.  
  
    |Valor|Configuração|Descrição|  
    |-----------|-------------------|-----------------|  
    |1|DISABLE_DEF_CNST_CHK|Controla a verificação provisória ou adiada de restrições.|  
    |2|IMPLICIT_TRANSACTIONS|Para conexões de biblioteca em rede dblib, controla se uma transação é iniciada implicitamente quando uma instrução é executada. A configuração IMPLICIT_TRANSACTIONS não tem nenhum efeito sobre conexões ODBC ou OLEDB.|  
    |4|CURSOR_CLOSE_ON_COMMIT|Controla o comportamento de cursores depois que uma operação de confirmação foi executada.|  
    |8|ANSI_WARNINGS|Controla truncamento e NULL em avisos de agregação.|  
    |16|ANSI_PADDING|Controla o preenchimento de variáveis do comprimento fixo.|  
    |32|ANSI_NULLS|Controla o tratamento de NULL ao usar operadores de igualdade.|  
    |64|ARITHABORT|Encerra uma consulta quando ocorre estouro ou erro de divisão por zero durante a execução da consulta.|  
    |128|ARITHIGNORE|Retorna NULL quando ocorre estouro ou erro de divisão por zero, durante a consulta.|  
    |256|QUOTED_IDENTIFIER|Faz a diferenciação entre aspas simples e duplas ao avaliar uma expressão.|  
    |512|NOCOUNT|Desativa a mensagem retornada ao término de cada instrução que declara quantas linhas foram afetadas.|  
    |1024|ANSI_NULL_DFLT_ON|Altera o comportamento da sessão para usar a compatibilidade ANSI para nulidade. Novas colunas definidas sem a nulidade explícita são definidas para permitir nulos.|  
    |2\.048|ANSI_NULL_DFLT_OFF|Altera o comportamento da sessão, para não usar a compatibilidade ANSI para nulidade. Novas colunas definidas sem a nulidade explícita são definidas para não permitir nulos.|  
    |4096|CONCAT_NULL_YIELDS_NULL|Retorna NULL ao concatenar um valor NULL com uma cadeia de caracteres.|  
    |8192|NUMERIC_ROUNDABORT|Gera um erro quando ocorre perda de precisão em uma expressão.|  
    |16384|XACT_ABORT|Reverte uma transação se uma instrução Transact-SQL ativar um erro em tempo de execução.|  
  
-   As posições de bit em **user options** são idênticas àquelas em @@OPTIONS. Cada conexão tem sua própria função @@OPTIONS, que representa o ambiente de configuração. Ao fazer logon em uma instância do \ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], um usuário recebe um ambiente padrão que atribui o valor atual de **user options** a @@OPTIONS. A execução de instruções SET para **user options** afeta o valor correspondente na função @@OPTIONS da sessão. Todas as conexões criadas depois que essa configuração foi alterada recebem o novo valor.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Permissões de execução sem parâmetros ou com apenas o primeiro parâmetro em **sp_configure** são concedidas a todos os usuários por padrão. Para executar **sp_configure** com ambos os parâmetros para alterar uma opção de configuração ou executar a instrução RECONFIGURE, o usuário deve ter a permissão ALTER SETTINGS no nível do servidor. A permissão ALTER SETTINGS é implicitamente mantida pelas funções de servidor fixas **sysadmin** e **serveradmin** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>Para configurar a opção de configuração user options:  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e selecione **Propriedades**.  
  
2.  Clique no nó **Conexões** .  
  
3.  Na caixa **Opções de conexão padrão** , selecione um ou mais atributos para configurar as opções de processamento de consulta padrão para todos os usuários conectados.  
  
     Por padrão, nenhuma opção de usuário está configurada.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-configure-the-user-options-configuration-option"></a>Para configurar a opção de configuração user options:  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) para configurar `user options` para alterar as configurações para a opção de servidor ANSI_WARNINGS.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'user options', 8 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
##  <a name="follow-up-after-you-configure-the-user-options-configuration-option"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar a opção user options configuration  
 A configuração entra em vigor imediatamente sem reiniciar o servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
