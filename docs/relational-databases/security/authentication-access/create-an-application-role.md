---
title: Criar uma função de aplicativo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.approle.general.f1
helpviewer_keywords:
- application roles [SQL Server], creating
ms.assetid: 6b8da1f5-3d8e-4f88-b111-b915788b06f1
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 09f90bcf10db6d5a1406aa7a68f90b4704270d95
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "72903156"
---
# <a name="create-an-application-role"></a>Criar uma função de aplicativo
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Este tópico descreve como criar uma função de aplicativo no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. As funções de aplicativo restringem o acesso do usuário a um banco de dados exceto quando feito por aplicativos específicos. As funções de aplicativo não têm nenhum usuário, assim a lista **Membros da Função** não é exibida quando é selecionada a **Função de aplicativo** .  
  
> [!IMPORTANT]  
>  A complexidade de Senha é verificada quando as senhas de função de aplicativo são definidas. Os aplicativos que invocam funções de aplicativo devem armazenar suas senhas. As senhas de função de aplicativo devem sempre ser criptografadas ao serem armazenadas.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para criar uma função de aplicativo usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER ANY APPLICATION ROLE no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
##### <a name="to-create-an-application-role"></a>Para criar uma função de aplicativo  
  
1.  No Pesquisador de Objetos, expanda o banco de dados onde você deseja criar uma função de aplicativo.  
  
2.  Expanda a pasta **Segurança** .  
  
3.  Expanda a pasta **Funções** .  
  
4.  Clique com o botão direito do mouse na pasta **Funções de Aplicativo** e selecione **Nova Função de Aplicativo...** .  
  
5.  Na caixa de diálogo **Função de Aplicativo – Nova**, na **Página Geral**, digite o novo nome da nova função de aplicativo na caixa **Nome da função**.  
  
6.  Na caixa **Esquema Padrão** , especifique o esquema que possuirá objetos criados por essa função digitando os nomes dos objetos. Como alternativa, clique nas reticências **(…)** para abrir a caixa de diálogo **Localizar Esquema**.  
  
7.  Na caixa **Senha** , digite uma senha para a nova função. Insira novamente essa senha na caixa **Confirmar Senha** .  
  
8.  Em **Esquemas de propriedade dessa função**, selecione ou confira os esquemas que serão de propriedade desta função. Um esquema pode ser de propriedade de um só esquema ou função.  
  
9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="additional-options"></a>Opções adicionais  
 A caixa de diálogo **Função de Aplicativo – Nova** também oferece opções em duas páginas adicionais: **Protegíveis** e **Propriedades Ampliadas**.  
  
-   A página **Protegíveis** lista todos os protegíveis e as permissões possíveis nesses protegíveis que podem ser concedidos ao logon.  
  
-   A página **Propriedades estendidas** permite adicionar propriedades personalizadas a usuários de banco de dados.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-an-application-role"></a>Para criar uma função de aplicativo  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- Creates an application role called "weekly_receipts" that has the password "987Gbv876sPYY5m23" and "Sales" as its default schema.  
  
    CREATE APPLICATION ROLE weekly_receipts   
        WITH PASSWORD = '987G^bv876sPY)Y5m23'   
        , DEFAULT_SCHEMA = Sales;  
    GO  
    ```  
  
 Para obter mais informações, veja [CREATE APPLICATION ROLE &#40;Transact-SQL&#41;](../../../t-sql/statements/create-application-role-transact-sql.md).  
  
  
